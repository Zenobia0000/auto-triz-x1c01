# TRIZ Knowledge Base — Prompt Markdown 參照表

## 用途

本資料夾存放 TRIZ 方法論的結構化參照表，以 Markdown 格式供 Copilot Prompt / RAG 上下文注入使用。
所有表格皆為**靜態知識**（TRIZ 經典理論幾乎不變），版本管理透過 Git 即可。

## 檔案清單

| 檔案 | 內容 | 筆數 | 用於策略流程步驟 |
|------|------|------|------------------|
| `01_39_parameters.md` | TRIZ 39 工程參數 | 39 筆 | Step 2 (TC 定義 — 改善/惡化參數對照) |
| `02_contradiction_matrix.md` | 39×39 矛盾矩陣 | 1,521 格 | Step 2 (TC → 發明原理查表匹配) |
| `03_40_principles.md` | TRIZ 40 發明原理 + 子原理 | 40 筆 | Step 2 (發明原理具體化為候選方向) |
| `04_separation_principles.md` | 物理矛盾分離原則 | 4 大類 | Step 3c (PC 分離策略選擇) |
| `05_76_standard_solutions.md` | Su-Field 76 標準解 | 76 筆 (5 大類) | Step 3d (SF 標準解匹配) / SF-only 快速通道 |

> **步驟編號對應 `docs/auto_triz_strategy.md` 的 Section 2 閉環推理流程。**

## 各步驟的知識庫載入時機

```
auto_triz_strategy.md 閉環流程
│
├── Step 1 (FA + SF 診斷)
│   └── 無需載入 KB（靠工程師建模）
│
├── Step 2 (TC → 候選方向)
│   ├── 📂 01_39_parameters.md — 將使用者描述的改善/惡化翻譯為標準參數
│   ├── 📂 02_contradiction_matrix.md — 用參數對查表，取得候選發明原理編號
│   └── 📂 03_40_principles.md — 將原理編號展開為具體解法方向
│
├── Step 3 (PC 深挖 + SF + 科學效應)
│   ├── 3a-3b: OZ-OT 鎖定 Px → 無需 KB
│   ├── 3c: 📂 04_separation_principles.md — 選擇分離策略
│   └── 3d: 📂 05_76_standard_solutions.md — SF 標準解匹配 + 科學效應導入
│
├── SF-only 快速通道（功能缺失，無矛盾）
│   └── 📂 05_76_standard_solutions.md — 直接用標準解補全功能
│
└── Step 4 (驗證)
    └── 無需載入 KB（靠四問判定）
```

## 使用方式

### 方式 1：全量注入 (小模型/短矩陣)
直接將對應 `.md` 檔內容放入 System Prompt 或 User Message 上下文。

### 方式 2：RAG 檢索注入 (推薦用於矛盾矩陣)
矛盾矩陣 39×39 佔大量 token，建議：
1. Step 2 確定改善/惡化參數後
2. 僅檢索矩陣中對應的 1-3 行注入上下文
3. LLM 從候選原理中選擇並具體化

### 方式 3：混合注入
- 39 參數 + 分離原則 + 40 原理 → 全量注入（token 可控）
- 矛盾矩陣 + 76 標準解 → RAG 按需檢索

## Token 估算

| 檔案 | 預估字元數 | 預估 token (中英混合) |
|------|-----------|---------------------|
| 39 參數 | ~3,000 | ~1,500 |
| 矛盾矩陣 (全量) | ~40,000 | ~15,000 |
| 矛盾矩陣 (單行) | ~500 | ~200 |
| 40 原理 | ~8,000 | ~4,000 |
| 分離原則 | ~2,000 | ~1,000 |
| 76 標準解 | ~12,000 | ~5,000 |
