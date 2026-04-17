# Auto-TRIZ Project Instructions

## TRIZ 工作流

本專案使用 Auto-TRIZ 閉環推理流程解決技術矛盾。所有 TRIZ 相關 skill/command 前綴為 `triz-`。

### 指令一覽

| 指令 | 用途 | 對應 Skill |
| :--- | :--- | :--------- |
| `/triz` | 主入口，自動路由到適當步驟 | triz-router |
| `/triz-scope` | Step 0: 問題定向 (5Why/KT/CECA) | triz-scoping |
| `/triz-model` | Step 1: 功能建模 (FA+SF) | triz-model |
| `/triz-solve` | Step 2+3: TC/PC/SF 解題 | triz-contradict |
| `/triz-verify` | Step 4: 驗證 + 下游交付 | triz-verify |
| `/triz-status` | 查看當前 TRIZ session 狀態 | (直接讀取 state) |

### 流程概覽

```
/triz [問題描述]
  │
  ├─ 有明確矛盾 → /triz-solve (TC 路徑)
  ├─ 功能缺失無副作用 → /triz-solve --sf-only
  ├─ 問題症狀 → /triz-scope → /triz-model → /triz-solve → /triz-verify
  └─ 無法判斷 → 引導式問答
```

### 知識庫

TRIZ 靜態參照表位於 `triz_knowledge_base/`，策略文件位於 `docs/auto_triz_strategy.md`。

### Session 狀態

TRIZ session 狀態持久化於 `.claude/context/triz/`。

## Skill 使用規則

遇到 TRIZ 相關問題時，**先透過 Skill tool 載入對應 triz-* skill 再行動**。

優先序：
1. **使用者明確指示** — 最高
2. **Skills** — 覆蓋預設系統行為
3. **預設系統提示** — 最低

## Agent

| Agent | 用途 |
| :--- | :--- |
| `triz-analyst` | TRIZ 分析推理（TC/PC/SF、矩陣查表、分離策略、SIM 評估）|
