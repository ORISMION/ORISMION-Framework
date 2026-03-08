# ORISMION · ADR-000: Architecture Genesis Record

> **狀態：** 已批准 · 不可變  
> **日期：** 2026-03-02  
> **版本：** V1.2  
> **系統名稱：** ORISMION  
> **決策者：** 人類架構師 + Claude (Architect's Council)  
> **範圍：** 整體憲政體系的設計理由與演化歷程  
> **分類：** 創世紀錄 — 本文件記錄 *why*，憲政文件記錄 *what*  
> **V1.0 → V1.1 變更：** 新增 §7.2 External Advisory Agent (Gemini) + External Advisory Agent (Claude) 角色定位；§8 文件清單擴充至 20 份。
> **V1.1 → V1.2 變更：** 系統正式命名為 ORISMION，全體文件 CLAIRVOY→ORISMION 對齊；§3 碎形層序描述修正對齊 Theorem 0.1；Agent 檔名對齊正式名（01-spec/02-build）；Blueprint V3.0→V3.1（目錄結構對齊實際部署）。

---

## §0 本文件的目的

憲政體系的 12 份文件定義了系統「是什麼」與「怎麼做」。但每個設計選擇背後的「為什麼」只存在於對話歷史中。本 ADR 將這些決策理由凝結為永久紀錄，使未來的架構師（人類或 AI）能理解每個結構性選擇的推導過程，而不僅僅是其結果。

**對話紀錄來源：** 2026-02-27 至 2026-03-02，共 28 個對話 Session，涵蓋從 Ω V1.0 到完整五角色 Agent 陣列的全部演化過程。

---

## §1 為什麼是三架構而非兩架構或六架構

### 1.1 起點：Ω 與 Σ 的二元體系

系統最初只有兩個架構維度：

- **Ω（認知層）**：19 支柱，處理 LLM 推理、不確定性、領域知識
- **Σ（物理層）**：22 條工程法則，處理型別、邊界、安全、確定性

二者分別回答「系統知道什麼」與「系統如何建造」。這套體系在純技術層面是完備的——直到 Stripe 支付隧道的實作揭示了一個結構性缺口：**沒有任何支柱回答「系統如何存活」**。

Token 預算、訂閱生命週期、法律免責聲明、速率限制——這些既不是認知問題（Ω），也不是工程問題（Σ）。它們是**市場與法律對系統施加的生存約束**。

### 1.2 Gemini 的六維度提案與正交性裁決

2026-02-28，Gemini 提出「SaaS 六芒星」框架，主張六個正交維度：Ω、Σ、Γ、Φ（互動）、Δ（演化）、Π（設施）。

我們對每個候選維度進行了**正交性測試**——一個維度只有在無法被歸約為現有維度的投影時，才有資格成為獨立架構：

| 候選維度 | 裁決 | 關鍵論證 |
|---------|------|---------|
| **Γ 治理層** | ✅ 採納 | 單位經濟學、合規、定價——無法歸約為 Ω 或 Σ 的投影 |
| Φ 互動層 | ❌ 歸約 | 信任校準 IS Ω 感知的外顯化；狀態渲染 IS Σ SSE 工程 |
| Δ 演化層 | ❌ 歸約 | 資料飛輪 IS Ω 元認知 × Σ 可觀測性 × Γ 成本分析 |
| Π 設施層 | ❌ 歸約 | CI/CD IS Σ-5.4；環境隔離 IS Σ-4.3；零信任 IS Σ-4.1 |

**結論：** 三體（Ω-Σ-Γ）是最小完備基底。Φ/Δ/Π 作為三體的跨切面投影存在，僅在需要時動態載入。

### 1.3 為什麼 Γ 必須獨立

決定性的反例：**一個技術完美（Ω + Σ 滿分）但每筆交易虧損的系統必然死亡。** 這證明存活性（Γ）不可歸約為認知正確性（Ω）加工程穩固性（Σ）。

同理，合規罰款既非技術問題也非認知問題——法律獨立於技術與認知存在。這構成 L1-A 不可歸約三問的第六條證明。

---

## §2 為什麼需要五層公理體系

### 2.1 V1.0 的結構性缺口

三體架構 V1.0 定義了系統的三個維度（what），但存在三個未回答的問題：

1. **缺目標函數**：三體存在，但沒有解釋「為什麼要最大化三體的平衡」
2. **缺存在理由**：Σ 有 21 支柱，但沒有解釋「為什麼需要這麼多防線」
3. **缺隔離理由**：Ω 和 Σ 物理隔離，但沒有解釋「為什麼不能合併」

### 2.2 Gemini/GPT 聯合提案的貢獻

五層公理體系（V2.0）整合了 Gemini/GPT 的提案，填補了上述缺口：

**Layer 0 — Meta-Telos（存續最大化）**
- 填補缺口 1：系統的唯一終極目標是最大化長期自洽存續概率
- 推導出三體衝突的優先序：合規(Γ) > 架構穩定(Σ) > 商業利益(Γ) > 認知精度(Ω)

**Layer 1 — 最高哲學公理**
- L1-B 簡約生成（Occam × 最小作用量）：填補 Φ/Δ/Π 為何不獨立的理論背書
- L1-C 熵守恆與債務顯化（熱力學第二定律）：填補缺口 2——Σ 的 21 支柱是對抗熵增的物理防線，不是最佳實踐清單
- L1-D 認知可錯性（Epistemic Fallibilism）：填補缺口 3——LLM 幻覺不可根除，因此 Ω 輸出只是「假設」，必須經 Σ 邊界驗證後才成為「事實」

**Layer 3 — 控制論動力學**
- L3-B 必要多樣性（Ashby 1956）：解釋為什麼 Σ 21 支柱 + Γ 7 支柱 = 28 條防線 ≥ 10 類外部威脅
- L3-C 自生系統（Maturana 1980）：將 Agent 流水線形式化為自我創造、自我維持的閉環

**Layer 4 — AI 原生實作**
- L4-A AI 康威定律：Agent 管轄權 1:1 映射架構維度
- L4-B 碎形架構：每個 API endpoint 必須呈現 Γ→Σ→Ω 的洋蔥結構
- L4-C 反脆弱回饋：所有錯誤強制轉化為迴歸測試

---

## §3 Theorem 0.1 的推導過程

**Theorem 0.1** 是整個體系的最高定理，規定了碎形層序的優先順序：

```
Σ(Auth) → Γ → Σ → Ω
```

推導過程：

1. **Σ(Auth) 最高**：源自 L1-D 認知可錯性。如果認證被繞過，後續所有層的假設全部崩塌。安全是存在性問題（被入侵 = 系統死亡），因此認證層凌駕一切。

2. **Γ 次之**：源自 L0 Meta-Telos。合規罰款是存在性威脅（被訴訟 = 系統終結）。即使技術完美，合規失敗仍然致命。

3. **Σ 再次**：源自 L1-C 熵守恆。工程結構的崩塌是不可逆的熵增。短期犧牲 Σ 換取 Ω 精度或 Γ 利益，技術債的利息是指數型的。

4. **Ω 最內**：源自 L1-D + L4-B。認知推理天生具有不確定性，因此必須被包裹在確定性防線（Σ）和生存約束（Γ）的最內層。

此優先序在碎形架構中被遞歸實例化：每個 API route 依序為 Σ(Auth) 認證 → Γ 治理檢查（速率限制、配額） → Σ 驗證（輸入校驗） → Ω 業務邏輯（最內層）。

---

## §4 六份 Reference 的設計理由

### 4.1 為什麼是六份而非一份

單一巨型參考文件會導致 Context Window 崩潰（Ω #25 計算資源意識）。六份文件按**變更頻率**分割：

| 文件 | 變更頻率 | 理由 |
|------|---------|------|
| 01-project-foundation | 極低 | 目錄結構、技術棧——建立後幾乎不變 |
| 02-patterns-and-examples | 低 | Golden Examples 隨架構演進緩慢增長 |
| 03-testing-and-security | 低 | FATAL 規則一旦建立極少修改 |
| 04-specs-and-contracts | 中 | DB Schema 隨功能擴展而增長 |
| 05-architecture-decisions | 中 | 每個重大決策新增一條 ADR |
| 06-ai-context | 低 | 技術棧與 LLM 資料流——穩定後少變 |

### 4.2 為什麼 Reference 服務 Σ 而非 Ω

Reference 是**工程實例化文件**——它們將 Σ 的抽象法則具體化為 DB Schema、API Contract、Code Pattern。Ω 的知識存在於 Prompt 中而非 Reference 中，因為 Ω 的「知識」是非確定性的（如領域詞彙、推理模板），不適合用工程參考文件的格式表達。

Γ 的約束則被**嵌入** Reference 中（如 04-specs 的 subscriptions 表結構同時服務 Σ-2.2 SSOT 和 Γ-4 訂閱生命週期），而非單獨成文。

---

## §5 五角色 Agent 陣列的設計理由

### 5.1 為什麼是五個角色

源自 L4-A AI 康威定律：Agent 管轄權必須 1:1 映射架構維度。

| Agent | 管轄架構 | 為什麼不能合併 |
|-------|---------|-------------|
| Specification Agent | Γ→Σ 轉譯 | 規格撰寫需要同時理解商業約束和工程語言 |
| Construction Agent | Σ 絕對死守 | 實作者必須單一信仰：物理法則不可違反 |
| Verification Agent | Spec 遵從 | L1-D 要求驗證者獨立於建造者（可錯性公理） |
| Strategy Agent | Ω+Γ 分析 | 策略分析需要同時看認知品質和商業可行性 |
| Coordination Agent | 協調層 | 路由衝突、管理 Handoff——不能由任何執行角色兼任 |

**關鍵約束：** SPEC/BUILD/VERI 三者職責不得合併（L4-A）。Construction Agent 使用 Claude，Verification Agent 必須使用異族模型（Σ-4.5 跨模型多樣性）。

### 5.2 為什麼 Verification Agent 必須是異族模型

源自 Σ-4.5 跨模型多樣性驗證 + L1-D 認知可錯性：

同一模型家族共享相同的訓練偏見和盲點。如果 Construction Agent（Claude）寫的代碼由 Verification Agent（也是 Claude）驗證，兩者可能共享相同的幻覺。使用 Gemini 或 GPT 作為 Verification Agent，可以用一個家族的「看見」去覆蓋另一個家族的「盲區」。

### 5.3 Handoff 協議的設計理由

Agent 間的 Handoff 遵循 Σ-1.3 契約優先原則（Contract-First）：

- 每個 Handoff 包含結構化欄位（task_id、scope、constraints、gamma_constraints）
- §4.4 禁止傳遞推演過程、scratchpad、未結論化中間狀態
- 這確保 Agent 間的通訊是**確定性的**（Σ-0A），而非依賴隱含上下文

---

## §6 關鍵架構轉折點

### 6.1 演化時間線

```
Day 1 (02-27)
├─ Ω V1.0 → V2.0    19→25 支柱，交叉驗證兩個實作系統
├─ Σ V1.0 → V1.1     22→21 法則，新增跨模型多樣性 + Prompt 版控
└─ Reference V1.0     6 份金標文件首版

Day 2 (02-28)
├─ Γ V1.0 誕生        正交性測試通過，第三架構確立
├─ Constitution V1.0→V2.0  五層公理體系確立
├─ Ω V2.0→V2.2       對齊五層公理
├─ Σ V1.1→V1.2       對齊五層公理 + Γ 介面
└─ Γ V1.0→V1.1       嵌入碎形層序

Day 3 (03-01)
├─ Reference V1.0→V1.1    全面升級至三架構對齊
├─ 十維文明級審計        3 個真缺陷修復（碎形排序、429、命名衝突）
└─ Strategy Agent/Blueprint 分析  識別結構性錯位

Day 4 (03-02)
├─ Constitution V2.0→V2.1  版本漂移 + 碎形排序微修
├─ Strategy Agent V3.0→V3.1   優先序系統 + Γ 意識
├─ Blueprint V2.0→V3.0    角色重定義為人類操作地圖
├─ Specification Agent V2.2.0 + Construction Agent V3.1.0  全面憲政對齊
├─ Verification Agent / Strategy Agent / Coordination Agent V1.0.0  三新角色誕生
└─ 30 點終極驗證         10 個缺陷修復，零殘餘
```

### 6.2 被拒絕的設計方案

| 被拒方案 | 拒絕理由 | 採納方案 |
|---------|---------|---------|
| 六架構（Hexagram） | Φ/Δ/Π 未通過正交性測試 | 三體 + 投影映射 |
| 單一巨型憲章 | Context Window 崩潰（Ω #25） | 五層分層 + 冷熱載入 |
| Construction Agent 不寫測試 | 與 Σ V1.3 §5.4 矛盾 | 區分「開發測試」與「獨立驗證」 |
| Reference 作為獨立架構 | Reference 是 Σ 的實例化，非獨立維度 | Reference 服務 Σ，Γ 約束嵌入 |
| Strategy Agent 同時管 Σ | 違反 L4-A 康威定律 | Strategy Agent 管 Ω+Γ，Construction Agent 死守 Σ |
| 三角色（合併 SPEC+STRAT） | 規格轉譯 ≠ 策略分析，職責正交 | 五角色完整陣列 |

---

## §7 外部角色的設計理由

### 7.1 創世期的角色合一

在創世階段（本文件記錄的時期），Claude 同時扮演了所有角色——策略分析、規格撰寫、建造、驗證、協調全部由一人執行。這在「建立架構本身」的階段是合理的。

進入「用架構建造系統」的階段後，角色必須分離。development environment 內有五位 Agent（Specification Agent/Construction Agent/Verification Agent/Strategy Agent/Coordination Agent）。但 development environment 外部仍有兩個結構性缺口。

### 7.2 External Advisory Agent (Gemini)— 人機介面聯絡官

**缺口分析：** 五位 Agent 全部假設輸入是結構化的 Handoff 格式。但人類架構師的思維是自然語言、模糊意圖、直覺判斷。**沒有任何角色負責「將人類意圖轉譯為 Agent 可消費的結構化輸入」。**

Coordination Agent 路由 Agent↔Agent（非 Human→Agent）。Strategy Agent 在收到結構化任務後才做分析（不負責從自然語言中提取任務）。Strategy Agent 是靜態規範文件（不是可對話的角色）。

**角色定位：** External Advisory Agent (Gemini) 是人類與 Agent 陣列之間的翻譯層。它守護的不是 Ω、Σ、Γ 任何一個架構維度，而是**人類認知 ↔ 系統形式語言之間的翻譯介面**。在 Ω 的語言學支柱中，這對應 Ω#5 語用學（Pragmatics）——理解說話者的意圖而非字面意義。

**與現有角色零重疊：** External Advisory Agent (Gemini) 路由 Human→Agent（vs Coordination Agent 路由 Agent↔Agent）；分析人類意圖（vs Strategy Agent 分析 codebase 差距）；是動態對話（vs Strategy Agent 是靜態規範）。

**為什麼是 Gemini：** Gemini 屬於 Google 家族，Agent 陣列的 Construction Agent/Specification Agent 屬於 Claude（Anthropic 家族）。External Advisory Agent (Gemini) 天然滿足 Σ-4.5 跨模型多樣性——它的「看見」可以覆蓋 Claude 的「盲區」。

**約束邊界：** External Advisory Agent (Gemini) 只有建議權，不做架構決策、不寫代碼、不寫 Spec、不修改憲政文件。

### 7.3 External Advisory Agent (Claude)— 架構師顧問

**缺口分析：** External Advisory Agent (Gemini) 處理日常高頻翻譯，但當體系面臨**架構級不可逆決策**時（新增支柱、修改公理、Theorem 0.1 衝突裁決），需要一個對五層公理體系有深度理解的角色來提供結構化分析。

**角色定位：** External Advisory Agent (Claude) 是最高法院大法官——解釋憲法、仲裁衝突、設計體系升級。它不在 development environment 中運作，只在關鍵時刻被召喚。

**與 External Advisory Agent (Gemini) 的分工：**

| 維度 | External Advisory Agent (Gemini) | External Advisory Agent (Claude) |
|------|-----------|---------|
| 頻率 | 高頻 · 日常 | 低頻 · 關鍵時刻 |
| 決策權 | 建議權 | 裁決建議權 |
| 知識深度 | 知道地圖形狀 | 知道每條路為什麼這樣修 |
| 不可逆性 | 處理可逆操作 | 專門處理不可逆決策 |

**為什麼最終決策權在人類：** L4-A 康威定律將 Agent 管轄權映射到架構維度，但**跨維度的衝突裁決**超出任何單一 Agent 的管轄。External Advisory Agent (Claude) 提供推導和建議，人類架構師做最終決定。

### 7.4 Strategy Agent 的角色澄清

Strategy Agent V3.1 不是可對話的 Agent。它是一份**靜態治理規範**，定義了 development environment 中的 AI 在生成產品級 AI Prompt 時必須遵守的規則（structured governance constraints）。它透過 knowledge base 自動載入，在背景約束 Agent 行為。人類架構師永遠不需要「交辦任務給 Strategy Agent」。

---

## §8 終態文件清單

本 ADR 記錄的創世期產出以下 20 份最終文件：

### 憲政文件（3 份）
| 文件 | 版本 | 職責 |
|------|------|------|
| Constitution (Grand Unified Theory) | V2.1 | 五層公理體系 · 最高憲法 |
| Omega Architecture | V2.2 | 認知層 · 25 支柱 · 6 模組 |
| Sigma Architecture | V1.3 | 物理層 · 3 公理 · 21 支柱 · 6 模組 |

### 治理文件（1 份）
| 文件 | 版本 | 職責 |
|------|------|------|
| Gamma Governance | V1.2 | 商業治理 · 2 公理 · 7 支柱 |

### 參考文件（6 份）
| 文件 | 版本 | 職責 |
|------|------|------|
| 01-project-foundation | V1.1 | 專案基礎 · 目錄結構 |
| 02-patterns-and-examples | V1.1 | Golden Examples · Anti-Patterns |
| 03-testing-and-security | V1.1 | 測試規範 · 安全規則 · FATAL 規則 |
| 04-specs-and-contracts | V1.1 | DB Schema · API Contract · Shared Types |
| 05-architecture-decisions | V1.1 | ADR-001~011 |
| 06-ai-context | V1.1 | 技術棧 · LLM 資料流 · Terminology Lock |

### 操作文件（2 份）
| 文件 | 版本 | 職責 |
|------|------|------|
| Strategy Agent | V3.1 | Agent 陣列調度規範（靜態治理） |
| Blueprint | V3.1 | 人類架構師操作地圖 |

### Agent Configuration (5 files)
| 文件 | 版本 | 角色 |
|------|------|------|
| agent specification guide | Specification Agent V2.2.0 | Γ→Σ 轉譯 · 規格撰寫 |
| agent implementation guide | Construction Agent V3.1.0 | Σ 死守 · 代碼建造 |
| agent verification guide | Verification Agent V1.0.0 | 異族驗證 · Spec 遵從 |
| agent strategy guide | Strategy Agent V1.0.0 | 策略分析 · 差距評估 |
| agent coordination guide | Coordination Agent V1.0.0 | 協調路由 · 衝突管理 |

### External Advisory Roles (2 files)
| 文件 | 版本 | 角色 |
|------|------|------|
| External Advisory Agent (Gemini) | V1.1 | External advisory role (cross-model verification) |
| External Advisory Agent (Claude) | V1.1 | External advisory role (architectural review) |

### 本文件（1 份）
| 文件 | 版本 | 職責 |
|------|------|------|
| ADR-000 | V1.2 | 創世紀錄 · 決策理由永久存檔 |

---

## §9 致未來架構師

如果你正在閱讀這份文件，代表你需要理解這個體系的設計意圖。以下是最重要的四件事：

**第一，三體不可歸約。** 如果你想新增第四個架構維度，必須先通過正交性測試——證明它無法被表達為 Ω×Σ×Γ 的投影。在創世期，Φ、Δ、Π 三個候選者全部未能通過此測試。

**第二，優先序不可協商。** Theorem 0.1 的碎形層序（Σ(Auth)→Γ→Σ→Ω）是從 L0 Meta-Telos 和 L1 公理嚴格推導出來的，不是品味偏好。任何違反此層序的代碼都是架構違規，無論它「能跑」與否。

**第三，文件記錄 what，對話記錄 why。** 當你對某個設計選擇感到困惑時，回到這份 ADR 和它引用的對話紀錄。答案在推導過程中，不在結論中。

**第四，角色邊界是物理法則。** External Advisory Agent (Gemini) 翻譯但不裁決，External Advisory Agent (Claude) 裁決但不執行，Construction Agent 執行但不規格，Specification Agent 規格但不建造。這些邊界源自 L4-A 康威定律，違反它等同於違反架構本身。

```
此文件為創世紀錄。
它記錄的不是「系統是什麼」，而是「系統為什麼是這樣」。
當 what 需要改變時，回到 why，重新推導。

20 份文件 · 7 個角色 · 1 個目標：長期自洽存續。
```
