# AICBD 面試分析：職缺解構與候選人定位架構

## 摘要

本職缺為台達電子先進工業電腦視覺解決方案新事業發展部（AICBD）之資深 AI 系統架構師，屬內部轉任情境。核心需求並非單一技術工種，而是具備「問題定義 → 系統設計 → 落地交付」完整路徑能力的複合型架構角色。候選人的適配性，取決於能否將製造現場的模糊痛點轉譯為可執行 AI 規格，並整合技術、流程、人機協作三個層面。

---

## 一、職缺需求解構

### 1.1 部門定位

AICBD 聚焦製造業人工作業問題，以 AI 與深度學習技術提供工業電腦視覺解決方案。三項核心目標：

| 目標 | 具體成效 |
| :--- | :--- |
| 提升組裝直通率 | AI 平台蒐集分析工站影像，減少錯漏反與重工 |
| 提高產品品質 | 關鍵步驟導入 AI 視覺檢測，穩定出貨品質 |
| 縮短新產品導入時間 | AI 技術加速新品導入流程 |

### 1.2 職缺性質

非純粹 Data Scientist 或 Backend Engineer，而是混合型架構角色，涵蓋：

| 能力類別 | JD 對應內容 |
| :--- | :--- |
| 系統架構設計 | AI 系統架構、模型訓練、推理、部署 |
| 技術導入優化 | 新 AI 技術導入、模型準確率與效率優化 |
| 問題解決 | 系統性能調優、技術瓶頸識別 |

### 1.3 技能需求（JD 明列）

| 技能項 | 對應層 |
| :--- | :--- |
| MLOps、Airflow、Kubeflow | 工作流編排與模型營運 |
| 後端框架 + ORM | 服務層 |
| RESTful API | 介面層 |
| RDB | 資料層 |
| Linux shell script | 基礎環境 |
| 獨立作業、溝通、學習能力 | 軟性條件 |

### 1.4 核心判準

職缺的決定性判準，並非特定工具熟練度，而是：**在雜亂、模糊、限制密集的工業場景中，將 AI 從概念推進為可持續運作系統的能力**。

### 1.5 情境特殊性

此為 **內部轉任**（台達電子現職員工轉 AICBD），意味著：

- 面試官可驗證候選人現行專案實績
- 重點在「既有能力如何遷移至 CV / 製造現場」
- 需主動處理「AI Agent / LLM 背景 → 工業電腦視覺」的遷移論述

---

## 二、候選人定位架構

### 2.1 定位層級

| 層級 | 描述 | 定位強度 |
| :--- | :--- | :--- |
| L1：Prompt Engineer | 會操作 LLM 工具 | 低，易被誤判 |
| L2：Model Developer | 會調參、訓練模型 | 中，可被替代 |
| L3：AI System Architect | 整合檢索、推理、流程、人機協作 | 高，貼近職缺需求 |
| L4：Problem Definer | 將模糊需求轉為可執行 SPEC | 高，稀缺能力 |

### 2.2 定位陳述

候選人適合的定位為 **AI 系統架構師 / 問題定義者 / 人機協作流程設計者**，完整敘述為：

> 將模糊、跨部門、資料不完整的問題，透過結構化拆解轉為具體 SPEC，並整合 AI、檢索、流程、自動化與人機審核機制為可交付系統。

---

## 三、候選人現有實績對照

此為候選人在台達既有職位（企業 AI Agent 平台架構師 & 技術負責人）之驗證實績，均可直接作為面試證據。

### 3.1 企業 AI Agent 平台（2024 – 至今）

| 項目 | 具體成果 |
| :--- | :--- |
| 企業研發 Copilot | 產品設計文件初稿 20 天 → 2 天（-90%） |
| Deep Research 引擎 | 異步多線並行，5–20 條平行搜尋代理；RCA 分析時間 -30% |
| System 1 / System 2 雙系統架構 | 依問題複雜度動態切換快取回應與鏈式推理 |
| 企業級 RAG 管線 | >10,000 份文件；多階段檢索（稀疏+稠密+重排序）；準確率 >80%；延遲 <1 秒 |
| OpenClaw + MCP 整合 | 工具標準化註冊、動態能力發現、跨代理共享 |
| TRIZ + 蘇格拉底推理層 | 結構化提問降低幻覺風險 |
| 可觀測性機制 | Agent trace、token 用量、工具成功率、幻覺偵測 |
| 多廠區落地 | 活躍使用者 >20，任務完成率 ≥80% |

### 3.2 MLOps & 智慧製造

| 項目 | 具體成果 |
| :--- | :--- |
| 地端 MLOps 架構 | 從雲端 SaaS 重構為地端系統，滿足資安合規 |
| 領域驅動 ML 模型部署 | 多製造廠區現場導入，產線痛點 → ML 解決方案 |
| 前瞻推動 | 2024 LLM 浪潮前主動提案並主導 Copilot 開發 |

### 3.3 實績與 JD 的對應

| JD 項目 | 候選人對應實績 |
| :--- | :--- |
| AI 系統架構設計 | Copilot + Deep Research + RAG 全鏈路 |
| 模型訓練、推理、部署 | 多廠區 ML 模型落地 |
| MLOps | 地端 MLOps 架構從 0 設計 |
| 後端 + API + RDB | RAG 管線、Agent 工具協議層 |
| Linux shell | 地端部署與資安合規工作 |
| 獨立作業 + 溝通 | 2024 前主動提案、跨廠區推進 |

---

## 四、能力地圖

### 4.1 硬能力（Hard Skills）

#### A. 問題定義與規格轉譯

**能力內容**
- 從非結構化需求中抽取目標、限制、評估方式
- 將現場語言翻譯為 AI 可執行的 SPEC
- 以結構化提問降低需求模糊與幻覺風險（已具體化為 TRIZ + 蘇格拉底推理層）

**對應 JD 價值**
- 縮短新產品導入時間
- 降低需求反覆確認成本
- 提升 PoC 成功率

#### B. AI / LLM / RAG 架構

**已落地實作**
- 10,000+ 文件企業級 RAG，準確率 >80%，延遲 <1s
- Multi-stage retrieval（稀疏+稠密+重排序）
- 對話感知 context management、文件級權限控制
- Agent workflow、System 1 / System 2 routing

#### C. MLOps / 部署 / 平台化

**已落地實作**
- 地端 MLOps 架構（資安合規）
- 多廠區 ML 模型部署
- Trace、token usage、tool success rate、hallucination detection

**JD 工具補強**
- Airflow、Kubeflow 為 JD 明列需求，需於面試中處理熟悉度議題（現有經驗偏 Agent 工作流，而非傳統 ML pipeline orchestration）

#### D. 自動化與工具編排

**已落地實作**
- Deep Research 多代理搜尋（5–20 並行）
- OpenClaw + MCP 服務整合
- 工具標準化註冊、動態能力發現
- 自動 RCA 報告產出（-30% 分析時間）

#### E. API / Backend / Data integration

**定位說明**
此能力非候選人最突出賣點，但已透過 RAG 管線、權限控制、MCP 協議層等專案累積實作經驗。需呈現「AI 系統無法脫離 backend 與 data layer 獨立存在」的系統觀。

---

### 4.2 軟能力（Soft Skills）

| 能力 | 本質 | 在此職缺的價值 |
| :--- | :--- | :--- |
| 模糊問題拆解 | 將混亂視為可定義的問題空間 | 架構師核心素質 |
| 跨功能翻譯 | 對主管、工程師、現場、使用者用不同語言表達同一件事 | 跨部門推動專案必要條件 |
| 主動提案與前瞻布局 | 2024 LLM 浪潮前主動推動導入 | 體現前瞻性與推動力 |
| 人機協作設計 | AI augment human，而非 AI replace human | 工業場域信任建立的必要條件 |
| 落地導向 | 以交付紀錄取代 vision 論述 | 與職缺「真實落地」需求對應 |

---

## 五、關鍵論述：LLM/Agent 經驗 → 工業電腦視覺的遷移

此為內部轉任最重要的論述，需主動處理。

### 5.1 表面落差

候選人現有實績偏 LLM / Agent / RAG；AICBD 主軸為電腦視覺。表面看似技術棧不重疊。

### 5.2 實質銜接

AICBD 的核心問題並非「做一個 CV 模型」，而是：

| AICBD 實際挑戰 | 候選人既有能力對應 |
| :--- | :--- |
| 組裝直通率分析：多工站影像 + 異常資料整合 | Multi-source retrieval、資料管線整合 |
| 現場不良率診斷 | RCA 自動化（已做過 -30% 驗證） |
| 新產品導入加速 | 需求定義 → SPEC 轉譯（Copilot 20→2 天驗證） |
| 現場標記成本高 | Human-in-the-loop、pre-labeling、confidence threshold |
| 多廠區差異 | 多廠區 ML 部署經驗、地端 MLOps |
| 工程師知識重用 | RAG 管線（>80% 準確率） |

### 5.3 論述句型

> AICBD 的挑戰不只是做出 CV 模型，而是讓 CV 成為製造現場可持續運作的系統能力。過去在企業 AI Agent 平台做的問題定義、系統整合、多廠區落地、可觀測性機制、人機協作設計，正是 CV 系統要落地必須處理的同一類問題。CV 模型本身是其中一個節點，但整套系統的架構能力是可遷移的。

---

## 六、面試敘事主線

### 6.1 主線一：對「好的企業 AI 架構師」的定義

> 好的企業 AI 架構師，不只是懂模型或框架，而是能在真實業務場景裡，把問題定義清楚、把資料和流程串起來、把 AI 系統設計成可持續運作的產品。在製造業，核心挑戰並非 benchmark，而是資料分散、場域差異、需求變動、現場信任。架構師的本質是整合技術、流程、人、資料與交付。

### 6.2 主線二：適配性三點

1. **問題定義能力** — 將模糊需求轉為具體規格（Copilot + TRIZ 推理層已驗證）
2. **系統整合能力** — RAG + Agent + MLOps + 可觀測性全鏈路（10,000 文件 / 多廠區已驗證）
3. **企業落地經驗** — 非 PoC，跨廠區推進與持續優化（活躍用戶 >20、任務完成率 ≥80% 已驗證）

### 6.3 主線三：過往貢獻（問題 → 做法 → 結果）

> 企業 AI Agent 平台的角色，是從 0 到 1 重新設計企業內知識工作流。當時最大問題不是模型強度，而是工程複雜度高、資料分散、知識查找成本高。設計整合 Agentic RAG、知識檢索、人機審核與 Deep Research 的架構，讓系統先拆解問題、跨來源搜尋、做初步評分，再產出可引用的結構化結果。結果：產品設計文件初稿時間 20 → 2 天（-90%），RCA 分析時間 -30%，多廠區落地，活躍使用者 >20。

### 6.4 主線四：未來 vision

> AI 在製造現場不應只做單點檢測，而應逐步成為支撐問題發現、知識檢索、異常判讀、標記協作、流程優化與持續學習的平台能力。工業電腦視覺的價值，不在模型準確率再提升幾個百分點，而在資料流、標記流、部署流、回訓流、現場決策流的串接。目標是將 AI 從「一次性專案」推進為「可複製的工業能力」。

---

## 七、關鍵題型標準答案架構

### 7.1 "What is the key factor of being a good AI architect?"

**英文版**
> The key factor is the ability to translate ambiguity into an executable system. In enterprise AI, especially in manufacturing, the challenge is rarely just model performance. The harder part is defining the real problem, aligning stakeholders, structuring messy data and workflows, and building a system that can actually be deployed, monitored, and improved over time. A good AI architect needs three things: problem framing, system thinking, and delivery capability.

**中文收斂**
> 把模糊變清楚，把技術變系統，把系統變成果。

### 7.2 "Why are you good at this?"

**英文版**
> One of my strongest advantages is problem definition. I'm good at taking unstructured requirements, unclear pain points, and fragmented information, and turning them into structured specifications, decision flows, and implementable AI workflows. In my current role, I embedded TRIZ and Socratic reasoning directly into the Copilot's dialogue design, to help engineers break down vague requirements before execution. This is not prompt engineering — this is specification design.

### 7.3 "Why were you able to contribute before LLM became mainstream?"

**英文版**
> In previous projects, I was able to contribute early because I start from problem framing and workflow design, not implementation. When the organization was still exploring AI, I proactively proposed the Copilot initiative before the 2024 LLM wave — when few inside the department were paying attention. That early contribution was possible because I had already been mapping the pain points in the engineering workflow and could see where LLM-driven agents would produce leverage.

### 7.4 "How does your LLM/Agent background transfer to computer vision?"

**英文版**
> The core challenge in AICBD is not building a single CV model — it's making CV a sustainable system inside the factory floor. The problems I've been solving — problem definition, multi-source data integration, on-prem MLOps for compliance, cross-site deployment, observability, and human-in-the-loop design — are exactly the non-model problems that any industrial CV system has to solve. The model is one node. The surrounding architecture is transferable.

### 7.5 "What's your vision for the future?"

**英文版**
> I see the future of enterprise AI as moving from isolated AI use cases to integrated decision-support systems. In manufacturing, this means AI should not only detect or predict, but also help people search, understand, troubleshoot, collaborate on labeling, and continuously improve the process. I want to contribute to building that bridge — from single models to scalable industrial AI capabilities.

---

## 八、代表性案例：非結構化資料 → SPEC 轉換流程

### 8.1 資料來源分類

| 類型 | 範例 |
| :--- | :--- |
| 結構化 | defect code、工站紀錄、MES/ERP 欄位、測試結果、時間戳、工單編號、不良類型 |
| 非結構化 | 工程師口述、現場抱怨、PDF 規格書、RCA 文件、維修紀錄、圖片/影片、Slack/email/meeting notes |

核心挑戰並非資料有無，而在 **如何將兩者轉為可執行 AI SPEC**。

### 8.2 SPEC 轉換流程

```text
Discover → Define → Spec → Design → Develop → Pilot Run → Fine Tune → Deliver → Monitor / Iterate
```

### 8.3 各階段內容

#### Step 1. Discover

問題焦點：誰痛、痛在哪、現行作法、最耗時 / 最易錯的節點、成功定義。

#### Step 2. Define

將現場語言轉為可執行任務。

**範例**

現場陳述：「資料很難找，問題來了都要翻很多報告。」

轉譯後 SPEC：
- 使用者：工程師 / RD / 品保
- 任務：快速找到與當前機型 / 異常現象相關的過往知識
- 輸入：自然語言問題 + 關鍵參數 + 機台型號
- 輸出：排序後文件、摘要、引用來源、候選 RCA
- KPI：查找時間、命中率、採納率

#### Step 3. Design

| 問題類型 | 對應資料 | AI 元件 | 人機協作點 |
| :--- | :--- | :--- | :--- |
| 資料搜尋困難 | 報告、PDF、規格書、RCA | RAG / search / reranker | 人工確認引用正確性 |
| 資料小量多樣 | 圖像、文字、表單 | few-shot / retrieval / active learning | 人工標記與修正 |
| 不良標記困難 | image + expert note | CV model + labeling UI | AI 預標、人員複核 |
| Troubleshooting 自動化 | log / issue / SOP | agent workflow / rule + LLM | 工程師最終判斷 |

### 8.4 完整案例：資料搜尋困難（已實作驗證）

**SPEC 轉譯**
- User: RD / FAE / 製程工程師
- Job-to-be-done: 異常發生時快速取得相關知識與案例
- Input: 問題描述、料號、模組名稱、異常現象
- Output: Top-k 文件、重點摘要、來源引用、類似案例
- Constraints: 權限控管、文件異質、低延遲
- KPI: 搜尋命中率、查找時間、使用率

**實際落地結果**
- 10,000+ 文件覆蓋
- 搜尋準確率 >80%
- 查詢延遲 <1 秒
- 文件級權限控制 + 對話感知 context management

---

## 九、JD 四大痛點的架構化對應

### 9.1 資料搜尋不易

**問題本質**：資料存在卻找不到、找到卻不能用、能用卻不可信。

**對應能力（已驗證）**：RAG（10,000+ 文件）、metadata、reranking、citation、permission control。

### 9.2 資料小量多樣

**問題本質**：製造場域資料小而雜、小而散，跨產品 / 跨站點差異大。

**對應能力**：task decomposition、few-shot、active learning、hybrid pipeline、domain adaptation。

### 9.3 不良標記上的人機協作

**問題本質**：AI 非完全取代人工，而是做預判、給候選、縮小範圍，由專家做高價值確認。

**對應能力**：human-in-the-loop、pre-labeling、review workflow、confidence threshold、feedback loop。

### 9.4 Trouble shooting 自動化

**問題本質**：故障排查存在大量重複性分析步驟。

**對應能力（已驗證）**：Deep Research（5–20 並行搜尋代理）、agent workflow、RCA assistant（-30%）、tool orchestration、observability。

---

## 十、面試節奏策略

### 10.1 三層結構

| 層級 | 目標 | 執行方式 |
| :--- | :--- | :--- |
| 第一層：建立角色認知 | 讓面試官快速理解候選人定位 | 自我介紹從定位切入，非技術堆疊 |
| 第二層：回答結構化 | 展現思維框架 | 問題 → 方法 → 結果 → 可複用能力 |
| 第三層：引導話題 | 將技術細節收攏回架構層級 | 「我會把它放回整體架構來看……」 |

### 10.2 自我介紹範本

> 目前在台達電子擔任企業 AI Agent 平台架構師與技術負責人，角色上涵蓋從問題定義、規格設計、系統流程、部署到人機協作機制。
>
> 最具代表性的工作，是將企業研發知識工作流重新設計為 AI Copilot 與 Deep Research 系統：設計文件初稿時間 20 天 → 2 天（降幅 90%），RCA 分析時間縮短 30%，建置超過 10,000 份文件的 RAG 管線，搜尋準確率 >80%、延遲 <1 秒，並在多廠區落地，活躍使用者超過 20 人。
>
> 一句話概括：擅長把複雜、模糊、跨部門的問題，整理為可落地的 AI 系統。這套方法論與 AICBD 在製造現場要解決的問題結構高度對應。

### 10.3 回答模板

1. 當時的問題
2. 拆解方式
3. 系統設計思路
4. 結果（量化）
5. 可複用能力收斂

---

## 十一、反問題庫

反問的目的是展現架構師思維高度。

| 反問 | 展現面向 |
| :--- | :--- |
| AICBD 在推動 AI 視覺方案時，最大瓶頸是資料面、模型面，還是導入與流程整合面？ | 理解真正問題未必在模型 |
| 現階段 CV 專案偏單點導入，還是已向平台化、可複製能力建設前進？ | 架構師對系統性思考的關注 |
| 標記、驗證與現場導入中，人與 AI 的分工如何設計？ | 對 human-in-the-loop 現實性的掌握 |
| 若此角色加入，前 6 個月最希望解決的問題為何？ | 實戰導向 |
| 企業 AI Agent 平台的架構能力，在 AICBD 期待如何被應用？ | 處理內部轉任的銜接議題 |

---

## 十二、面試作戰地圖

### 12.1 定位標籤

**採用**
- 問題定義型 AI 架構師
- 企業 AI 系統整合者
- 模糊需求 → 可落地 SPEC 的轉譯者
- 人機協作與場域落地設計者

**避免**
- Prompt engineer
- 會用 LLM 的人

### 12.2 三項核心賣點

1. **定義問題**：非結構化需求 → 可執行 SPEC（TRIZ + 蘇格拉底推理層已具體實作）
2. **系統整合**：RAG（>10K 文件、>80% 準確率）+ Agent + MLOps + 可觀測性的完整串接
3. **企業落地**：跨廠區、跨角色、跨流程導入，活躍使用者 >20，任務完成率 ≥80%

### 12.3 節奏

1. 先定義身分
2. 再講解題方式
3. 再講成果（用量化數據）
4. 最後講 vision 與遷移論述

### 12.4 核心口訣

> 問題先定義，資料再整理，AI 才部署。

---

## 十三、風險議題與預先處理

### 13.1 JD 工具熟悉度落差

**議題**：JD 明列 Airflow、Kubeflow；候選人現有經驗偏 Agent 工作流編排，未必精熟傳統 ML pipeline orchestration。

**處理論述**
> 過去在地端 MLOps 系統中處理的是資安合規下的多廠區部署流程，使用的編排工具取決於場域限制。Airflow / Kubeflow 屬同類範疇的編排框架，核心概念（DAG、依賴管理、重試、監控）已在既有系統中實作，工具切換屬執行層，非架構層。

### 13.2 LLM/Agent → CV 的跨域議題

**議題**：既有實績偏 LLM，AICBD 主軸為 CV。

**處理論述**：見第五章遷移論述。

### 13.3 內部轉任的動機陳述

**議題**：為何離開現職轉 AICBD？

**論述方向**
- 既有能力在 AICBD 問題結構上有更大槓桿
- CV + 現場資料是 AI 架構能力的下一個應用場域
- 從知識工作流轉向實體製造流程，拓展系統落地的完整性

---

## 十四、本質陳述

AI 架構師的本質是 **將混亂轉為秩序**：盤點資源位置、區分優先序、規劃路徑、降低協作與維運摩擦。其價值不在單一工具能力，而在系統性的整合。

此職缺的三個支柱：

1. 問題定義先於技術展示
2. AI 系統化而非僅是模型
3. 人機協作與真實落地為評判標準

候選人實績（Copilot 20→2 天、RCA -30%、RAG >80%、多廠區 >20 用戶）已對這三個支柱完成初步驗證；面試核心任務是將此能力結構明確遷移到 AICBD 的 CV 場域。
