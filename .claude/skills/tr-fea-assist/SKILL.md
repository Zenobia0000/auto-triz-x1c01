# TR FEA 設定輔助

## Overview

本 skill 輔助工程師設定和判讀 FEA/CFD 分析，覆蓋電磁、結構、熱流三大域。提供材料卡指定、邊界條件、網格策略、收斂準則、常見陷阱，並可產出求解器 input snippet。

**宣告：** 「正在使用 tr-fea-assist skill — 輔助 {WI/domain} 的 FEA 設定。」

---

## 輸入

```
/tr-fea WI-01              # 針對 WI-01 (AFM 磁路) 的 FEA 輔助
/tr-fea WI-02              # 針對 WI-02 (諧波齒輪) 的 FEA 輔助
/tr-fea WI-03              # 針對 WI-03 (PCM 熱管理) 的 FEA 輔助
/tr-fea motor              # 以子系統名稱指定
/tr-fea result WI-01       # 判讀 WI-01 的 FEA 結果
```

| 參數 | 必要 | 說明 |
|:-----|:-----|:-----|
| WI-nn 或 domain | 是 | 目標 WI 或子系統（motor/gearbox/thermal/structural） |
| result | 否 | 切換到結果判讀模式 |

---

## 行為

### Phase 1: 載入上下文

1. 讀取目標 WI 文件（`docs/engineering/work_instructions/WI-xx_*.md`）
2. 讀取對應 Material Card（`docs/engineering/material_cards/MC-xx_*.md`）
3. 讀取 `.tr-state.json` 取得 WI 狀態和已完成步驟
4. 讀取 `docs/engineering/tr_gate_framework.md` 取得目標 gate 退出條件中的 FEA 判定標準

### Phase 2: 輔助輸出（依 domain 分支）

---

### Domain A: 電磁 FEA (WI-01 — AFM 磁路)

**求解器**: JMAG / ANSYS Maxwell / Motor-CAD

#### 材料卡指定

| 組件 | 材料 | MC 檔案 | 關鍵輸入 |
|:-----|:-----|:--------|:---------|
| 永磁鐵 | NdFeB N42SH | MC-01 | Br=1.30T, μ_r=1.05, Hcj≥1592kA/m, 溫度係數 |
| 定子芯 | SMC Somaloy 700 5P | MC-02 | B-H 曲線(15 點)、Steinmetz 參數、各向同性 k=20 W/mK |
| 轉子鐵芯 | S45C or SMC | (需建立) | B-H 曲線 |

#### 邊界條件

```
模型策略:
├─ 2D 快速迭代: 1/8 模型（利用 8 極對稱），週期性 BC
├─ 3D 精確: 1/4 模型，master/slave 週期性，含端部效應
└─ 軸向力分析: 必須 3D，磁石偏移 ±0.1mm 參數掃描

載荷步:
1. 空載（Bg 分布、反 EMF、鐵損）
2. 額定（5Nm, MTPA 角度掃描，銅損+鐵損）
3. 峰值（7Nm @3sec, 暫態溫升）
4. 場弱（3000rpm, 弱磁角度 vs 效率）
5. 軸向力（磁石偏位 ±0.1mm 敏感度）
```

#### 網格策略

| 區域 | 網格尺寸 | 理由 |
|:-----|:---------|:-----|
| 氣隙 | ≤ 0.2mm（至少 3 層） | 磁通密度梯度最大 |
| 永磁鐵 | ≤ 1.0mm | 退磁分析精度 |
| SMC 定子齒 | ≤ 0.5mm | 鐵損計算精度 |
| 轉子鐵 | ≤ 2.0mm | 低梯度區域 |
| 繞組 | ≤ 1.0mm | 銅損分布 |

#### 收斂準則

- 非線性迭代: 殘差 < 1e-4, 最大迭代 100
- 暫態步長: 電角度 1°（= 機械角 0.125°@8 極）
- 氣隙 Bg 變化 < 0.5% between mesh refinements

#### Pass/Fail 標準（對應 TR0→TR1）

| 指標 | Pass 條件 | 來源 |
|:-----|:---------|:-----|
| 氣隙 Bg | ≥ 0.8T | WI-01 設計輸入 |
| 額定扭矩 | ≥ 5.0 Nm | WI-01 設計輸入 |
| 峰值扭矩 | ≥ 7.0 Nm @3sec | WI-01 設計輸入 |
| 效率 @額定 | ≥ 90% | WI-01 設計輸入 |
| 鐵損 @3000rpm | ≤ 20W | WI-01 / V4 判定 |
| 軸向力 @±0.1mm | < 推力軸承額定/2 | 風險 R-001 |

#### 常見陷阱

1. **SMC B-H 曲線**: 不要用矽鋼片數據代替；SMC 飽和點更低（~1.5T vs 2.0T）
2. **3D 端部效應**: AFM 的漏磁主要在軸向端部，2D 模型會高估扭矩 10-15%
3. **溫度退磁**: N42SH @150°C 的 Br 降至 ~1.10T，退磁分析必須用高溫 B-H
4. **鐵損分離**: SMC 的磁滯損與渦流損比例不同於矽鋼片，確認 Steinmetz 參數來源

---

### Domain B: 結構 FEA (WI-02 — 齒輪 + WI-04 — 殼體)

**求解器**: ANSYS Mechanical / Abaqus / SolidWorks Simulation

#### WI-02 齒輪分析

**材料卡指定:**

| 組件 | 材料 | MC 檔案 | 關鍵輸入 |
|:-----|:-----|:--------|:---------|
| 柔輪 | CoCrMo F1537 wrought | MC-03 | σ_y=1000MPa, E=240GPa, Goodman 疲勞數據 |
| 剛輪 | CF-PEEK 30%CF | MC-04 | **各向異性**: 射出流向 vs 垂直向，Weld line 強度折減 |

**邊界條件:**

```
分析類型:
├─ 靜態: 柔輪齒根應力 @125Nm（最大嚙合載荷）
├─ 疲勞: Goodman diagram, R=-1 彎曲 @10,000 cycles
├─ 接觸: 柔輪-剛輪齒面接觸應力（Hertz）
└─ 模態: 嚙合頻率 vs 結構固有頻率（避免共振）

載荷施加:
- 柔輪: 橢圓變形 + 齒面分佈載荷（非簡單集中力）
- 剛輪: 齒根彎曲 + 齒面赫茲接觸
- 波發生器: 凸輪曲線預載
```

**網格策略:**

| 區域 | 網格 | 理由 |
|:-----|:-----|:-----|
| 柔輪齒根 | ≤ 0.1mm (hex preferred) | 應力集中，疲勞關鍵 |
| 齒面接觸 | ≤ 0.05mm | 赫茲接觸寬度 ~0.1mm |
| 柔輪筒壁 | ≤ 0.5mm (4+ 層) | 彎曲應力梯度 |
| 剛輪本體 | ≤ 1.0mm | 低梯度 |

**Pass/Fail 標準:**

| 指標 | Pass 條件 | 來源 |
|:-----|:---------|:-----|
| 柔輪 von Mises | < σ_y / 3 = 333 MPa | WI-02, 安全係數 3× |
| 剛輪齒根應力 | ≤ 150 MPa | WI-02 設計輸入 |
| 疲勞安全係數 | ≥ 1.5 @10,000 cycles | Goodman diagram |
| 接觸應力 | ≤ 800 MPa | CoCrMo 接觸疲勞限 |

**常見陷阱:**

1. **CF-PEEK 各向異性**: 射出流向 σ=380MPa vs 垂直方向 ~200MPa，齒根取最弱方向
2. **柔輪預載**: 波發生器的橢圓預載是柔輪應力的主要來源，不可省略
3. **Weld line**: CF-PEEK 射出件的 weld line 強度僅為 bulk 的 50-70%
4. **CoCrMo 加工殘餘應力**: wrought → machined 表面有拉伸殘餘應力

#### WI-04 殼體分析

**材料卡指定:**

| 組件 | 材料 | MC 檔案 | 關鍵輸入 |
|:-----|:-----|:--------|:---------|
| 殼體 | AZ91D-T6 | MC-05 | σ_y=150MPa(cast), E=45GPa, 蠕變 >120°C |
| 嵌件 | SUS304 | (需建立) | σ_y=205MPa, E=193GPa |

**分析重點:**

```
1. 扭矩反力路徑: 125Nm → 齒輪箱→殼體→車架（螺栓載荷）
2. 軸承座應力: 主軸承 + 推力軸承座剛性
3. 薄壁 (2.5mm) 變形: PCM 腔體區域壁厚更薄
4. 嵌件拔出力: SUS304 嵌件 vs AZ91D 界面（PEO 塗層後）
5. 模態分析: 避免齒輪嚙合頻率激勵
```

---

### Domain C: 熱流 FEA (WI-03 — PCM 熱管理)

**求解器**: ANSYS Fluent / COMSOL / Star-CCM+

#### 材料卡指定

| 組件 | 材料 | MC 檔案 | 關鍵輸入 |
|:-----|:-----|:--------|:---------|
| PCM | RT55 | MC-06 | Enthalpy-Temperature 曲線、Solidus=45°C/Liquidus=57°C |
| 殼體 | AZ91D | MC-05 | k=72 W/mK |
| 定子 | SMC | MC-02 | k=20 W/mK (isotropic) |

#### 邊界條件

```
模型策略:
├─ 穩態初篩: 僅固體導熱（無 PCM 相變），快速確認熱路徑
├─ 暫態精確: 含 PCM 相變（enthalpy-porosity method），8min 連續工況
└─ 恢復分析: 斷電後自然對流，PCM 固化 + 殼體散熱

熱源:
- 馬達銅損: 定子繞組體積熱源（W/m³）← WI-01 loss map
- 馬達鐵損: 定子芯體積熱源 ← WI-01 loss map
- 齒輪箱摩擦熱: 齒面接觸面熱通量（W/m²）← WI-02 效率
- 驅動板損耗: PCB 表面 ~10W ← 估算

外部:
- 自然對流: h = 10-15 W/m²K（靜止空氣，殼體外壁）
- 輻射: ε = 0.85（黑色塗裝）
- 環境溫度: 25°C（標準）/ 40°C（最惡劣）
```

#### 網格策略

| 區域 | 網格 | 理由 |
|:-----|:-----|:-----|
| PCM 腔體 | ≥ 5 層（厚度方向） | 相變前沿解析，MC-06 要求 |
| 殼體壁 | 3 層 | 壁面溫度梯度 |
| 氣隙 | 2 層 | 熱阻層 |
| 空氣域（自然對流）| 壁面第一層 y+ < 1 | 自然對流邊界層 |

#### 收斂準則

- 能量殘差 < 1e-6
- 暫態步長: 5-10 秒（8min 工況需 48-96 步）
- 監測點: 殼體最高溫、PCM 液相比例、定子最高溫

#### Pass/Fail 標準

| 指標 | Pass 條件 | 來源 |
|:-----|:---------|:-----|
| 殼體最高溫 @8min (25°C) | ≤ 80°C | WI-03 / TR1 退出 |
| 殼體最高溫 @8min (40°C) | ≤ 90°C | WI-03（可放寬） |
| PCM 液相比例 @8min | < 100%（未完全融化）| WI-03 設計餘量 |
| 恢復時間 (80°C → 57°C) | ≤ 15 min | WI-03 使用場景 |
| 定子最高溫 | ≤ 150°C（N42SH 退磁邊界）| MC-01 |

#### 常見陷阱

1. **PCM 自然對流**: 融化後的液態石蠟有自然對流，thin cavity 中 Ra 數低可忽略，但需確認
2. **熱界面電阻**: 殼體↔定子 的接觸熱阻顯著，不可假設完美接觸（用 TIM 或 gap conductance）
3. **PCM 過冷**: RT55 有 ~2°C 過冷，影響固化起始溫度
4. **AZ91D 蠕變**: 殼體溫度 >120°C 時 AZ91D 蠕變顯著，但正常工況不應到此溫度

---

## Phase 3: 結果判讀模式

當使用者使用 `result` 參數時：

1. 請使用者提供 FEA 結果（截圖、數據表、或文字描述）
2. 對比 Phase 2 中定義的 Pass/Fail 標準
3. 產出判讀報告：

```markdown
## FEA 結果判讀 — {WI-nn}

### 結果摘要

| 指標 | FEA 值 | Pass 條件 | 判定 | 備註 |
|:-----|:-------|:---------|:-----|:-----|
| {metric} | {value} | {criterion} | PASS/FAIL | {note} |

### FEA vs WI 預測對比

| 參數 | WI 預測/估算 | FEA 結果 | 偏差 | 評估 |
|:-----|:-------------|:---------|:-----|:-----|
| {param} | {predicted} | {fea_result} | {delta_pct}% | OK / 需檢查 |

### 建議下一步

{基於結果的具體建議}
```

4. 更新 `.tr-state.json` 的 WI 狀態

---

## Phase 4: 求解器 Input Snippet（可選）

使用者可要求產出特定求解器的 input file 片段：

| 求解器 | 支援片段 |
|:-------|:---------|
| ANSYS APDL | 材料定義、載荷步、網格控制 |
| ANSYS Fluent (UDF/TUI) | PCM enthalpy-porosity 設定 |
| Abaqus | *MATERIAL, *STEP, *BOUNDARY |
| JMAG | 材料 B-H table import |
| COMSOL | Phase change module 設定 |

**注意**: Snippet 僅為起點，使用者必須根據實際模型調整。每個 snippet 附帶「使用前請確認」清單。

---

## 狀態更新

FEA 完成後更新 `.tr-state.json`：

```json
{
  "wi_status": {
    "WI-01": {
      "status": "in_progress",
      "steps_completed": ["fea_setup", "fea_run"],
      "deliverables": {
        "loss_map": "pending",
        "axial_force_report": "pending"
      }
    }
  }
}
```

---

## 下一步導引

| 狀態 | 提示 |
|:-----|:-----|
| FEA 設定完成 | 「FEA 設定已輸出。執行模擬後，使用 `/tr-fea result WI-xx` 判讀結果。」 |
| FEA 結果全 pass | 「WI-xx FEA 全部通過。此子系統已具備 TR1 條件。執行 `/tr-gate TR1` 進行 gate review。」 |
| FEA 結果有 fail | 「{指標} 未通過（{actual} vs {required}）。建議: {specific_action}。」 |
