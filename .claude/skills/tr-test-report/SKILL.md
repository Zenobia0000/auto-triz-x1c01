# TR 測試報告產生器

## Overview

本 skill 協助工程師產出 V-test 和 DVP&R 測試報告，引導數據輸入、判定 pass/fail、執行 FEA correlation、更新風險狀態。

**宣告：** 「正在使用 tr-test-report skill — 產出 {test_id} 測試報告。」

---

## 輸入

```
/tr-test V1                # 產出 V1 (AFM 靜態扭矩) 測試報告
/tr-test V5-V8             # 產出 Phase B 全部測試報告
/tr-test phase-A           # 產出 Phase A (馬達) 全部測試報告
/tr-test all               # 產出所有已完成測試的報告
/tr-test dvpr              # 產出 DVP&R 總表（TR9 用）
```

| 參數 | 必要 | 說明 |
|:-----|:-----|:-----|
| Vn / Vn-Vm / phase-X / all / dvpr | 是 | 目標測試項 |

---

## 行為

### Phase 1: 載入測試規格

1. 讀取 `docs/engineering/work_instructions/WI-06_prototype_build_test.md`
2. 找到目標 V-test 的規格（方法、判定標準、設備需求）
3. 讀取 `.tr-state.json` 取得測試項目現有狀態

### Phase 2: 數據收集

引導使用者輸入實測數據。對每個 V-test 項目：

```markdown
## V{n}: {test_name}

請提供以下實測數據：

| 需要資料 | 格式 | 範例 |
|:---------|:-----|:-----|
| {data_1} | {format} | {example} |
| {data_2} | {format} | {example} |
...

測試條件:
- 日期: ___
- 設備: ___
- 環境溫度: ___°C
- 操作者: ___
- 備註: ___
```

**各 V-test 需要的數據:**

| V-test | 需要數據 |
|:-------|:---------|
| V1 靜態扭矩 | 鎖轉電流(A), 量測扭矩(Nm), MTPA 角度(°) |
| V2 氣隙磁通 | 反 EMF 波形(V vs rpm), 計算 Bg(T) |
| V3 軸向力 | 軸向力 vs 電流(N vs A), 軸向力 vs 轉速(N vs rpm) |
| V4 SMC 鐵損 | 空載輸入功率(W) @多轉速, 機械損扣除(W) |
| V5 噪聲 | SPL @1m dB(A), 1/3 octave 頻譜 |
| V6 齒輪效率 | 輸入/輸出扭矩(Nm) × 轉速(rpm) @多工況 |
| V7 柔輪疲勞 | 已完成循環數, 裂紋檢測結果, 應變計數據 |
| V8 齒根應力 | 應變計量測值(MPa) @125Nm |
| V9 總重量 | 各組件重量(g), 總重(g) |
| V10 溫升 | 殼體各點溫度 vs 時間曲線, 環境溫度 |
| V11 同心度 | CMM 量測值(mm) |
| V12 防腐蝕 | 鹽霧時數, 腐蝕面積(%), 拍照記錄 |
| V13 PCM 循環 | 初始 ΔH(kJ/kg), 循環後 ΔH(kJ/kg), 循環數 |
| V14 EMI | 頻譜數據, ADC SNR(dB) |

### Phase 3: 判定

對每個 V-test：

| 判定 | 條件 |
|:-----|:-----|
| **PASS** | 實測值滿足 WI-06 判定標準 |
| **MARGINAL** | 實測值在判定標準的 90-100% 範圍 |
| **FAIL** | 實測值未滿足判定標準 |

**判定標準（從 WI-06 提取）:**

| V-test | Pass 條件 |
|:-------|:---------|
| V1 | 扭矩 ≥ 5.0 Nm |
| V2 | Bg ≥ 0.8T (間接), FEA 偏差 < 10% |
| V3 | F_axial < 推力軸承額定 / 2 |
| V4 | 鐵損 ≤ 20W @3000rpm |
| V5 | SPL ≤ TQ HPR50 基準 |
| V6 | 效率 ≥ 85% @額定 |
| V7 | ≥ 10,000 cycles 無裂紋 |
| V8 | 齒根應力 ≤ 150 MPa |
| V9 | 總重 ≤ 2500g |
| V10 | 殼溫 ≤ 80°C @25°C環境/8min |
| V11 | 同心度 ≤ 0.05mm (per ICD-04) |
| V12 | 1000h 鹽霧無紅鏽 (per WI-08) |
| V13 | PCM ΔH 衰退 ≤ 5% @1000 cycles |
| V14 | ADC SNR ≥ 60dB |

### Phase 4: FEA Correlation

對有 FEA 預測值的 V-test，計算偏差：

```
偏差 = |實測值 - FEA 值| / FEA 值 × 100%
```

| 偏差範圍 | 評估 | 動作 |
|:---------|:-----|:-----|
| ≤ 10% | 良好 | FEA 模型可信 |
| 10-20% | 可接受 | 記錄偏差原因，模型微調 |
| > 20% | **需修正** | 標紅，FEA 模型必須修正後才能用於後續分析 |

### Phase 5: 產出報告

報告輸出到 `docs/engineering/test_reports/V{n}_report_{YYYY-MM-DD}.md`：

```markdown
# V{n} 測試報告: {test_name}

> **日期**: {test_date}
> **報告產出**: {YYYY-MM-DD}
> **判定**: {PASS / MARGINAL / FAIL}
> **TRIZ Session**: {triz_session_ref}
> **對應 WI**: WI-06 Phase {X}

---

## 測試條件

| 項目 | 內容 |
|:-----|:-----|
| 設備 | {equipment} |
| 環境溫度 | {temp}°C |
| 操作者 | {operator} |
| 日期 | {date} |

## 測試結果

| 量測項 | 實測值 | 判定標準 | 判定 |
|:-------|:-------|:---------|:-----|
| {metric} | {measured} | {criterion} | PASS/MARGINAL/FAIL |

## FEA Correlation

| 參數 | FEA 預測 | 實測值 | 偏差 | 評估 |
|:-----|:---------|:-------|:-----|:-----|
| {param} | {fea} | {measured} | {delta}% | {assessment} |

## 數據附件

{原始數據表、圖表、照片等}

## 觀察與建議

{測試過程觀察、異常現象、改善建議}

---

## 風險影響

| 風險 ID | 測試前狀態 | 測試後建議 | 理由 |
|:--------|:-----------|:-----------|:-----|
| {risk_id} | {before} | {after} | {reason} |
```

### Phase 6: DVP&R 總表（TR9 用）

當使用者輸入 `dvpr` 時，彙整所有 V-test + PV 測試為 DVP&R 總表：

```markdown
# DVP&R — Design Verification Plan & Report

> **產品**: e-Bike Drive Unit v2
> **日期**: {YYYY-MM-DD}

| # | 測試項目 | 規格 | 方法 | 樣本數 | Alpha 結果 | PV 結果 | 判定 |
|:--|:---------|:-----|:-----|:-------|:-----------|:--------|:-----|
| V1 | 靜態扭矩 | ≥5.0Nm | 鎖轉 | 3 | {result} | {result} | {P/F} |
| V2 | 氣隙磁通 | ≥0.8T | 反EMF | 3 | {result} | {result} | {P/F} |
...
| V14 | EMI | SNR≥60dB | 頻譜 | 3 | {result} | {result} | {P/F} |
| D1 | 耐久 | 10萬×125Nm | 循環 | 3 | — | {result} | {P/F} |
| D2 | 環境 | -20~+50°C | 溫箱 | 3 | — | {result} | {P/F} |
| D3 | 安全 | EN15194 | 認證 | 3 | — | {result} | {P/F} |
| D4 | 防水 | IP67 | 浸水 | 3 | — | {result} | {P/F} |
```

---

## 狀態更新

測試完成後更新 `.tr-state.json`：

1. **v_tests**: 更新狀態和結果
```json
{
  "V1": { "status": "tested", "result": "pass", "date": "2026-MM-DD", "report": "docs/engineering/test_reports/V1_report_2026-MM-DD.md" }
}
```

2. **risk_status**: 根據測試結果調整
   - V-test pass → 對應風險降級（如 R-001 從 open → mitigated）
   - V-test fail → 對應風險升級 + 標記 blocker

3. **subsystem_tr**: 若 Phase 全部 pass → 更新子系統 TR

---

## 下一步導引

| 狀態 | 提示 |
|:-----|:-----|
| Phase 全 pass | 「Phase {X} 全部通過。下一步: Phase {X+1}。或執行 `/tr-gate TR6` 進行 Alpha 驗證 gate review。」 |
| 有 fail 項 | 「V{n} 未通過。{失敗對策}。修正後使用 `/tr-test V{n}` 重測。」 |
| 全部 V-test pass | 「V1-V14 全部通過！Alpha 驗證完成。執行 `/tr-gate TR6`。」 |
| DVP&R 完成 | 「DVP&R 全項通過。執行 `/tr-gate TR9` 進行量產驗證 gate review。」 |
