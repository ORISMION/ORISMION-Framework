# ORISMION · Σ 架構 — 物理層與軟體工程底層理論總表 V1.3

## Sigma-Architecture: The 21 Pillars of Deterministic Engineering

> **上位法源：** 00-grand-unified-theory.md V2.1 — 終極憲章
> **憲章定位：** Σ = 三體之身體。管轄一切確定性工程。
> **憲章公理依據：** L1-C 熵守恆（Σ 的存在理由）× L1-A Q2「如何維持秩序」× L1-D 認知可錯性（Ω↔Σ 隔離理由）
> **升級基線：** V1.2 + ADR-027 (ADR-027) 前沿架構融合對齊
> **管轄範圍：** 型別安全、邊界解耦、網路物理、安全縱深、演化可逆、可觀測性 — 一切確定性工程
> **禁止越權：** Σ 不做推理(Ω)、不做定價(Γ)、不做置信度判斷(Ω)

---

## V1.1 → V1.2 變更摘要

| 變更類型 | 項目 | 來源 |
|---------|------|------|
| **新增 §0.1** | 公理層憲章回溯：L1-C 熵守恆 | 憲章 L1-C |
| **新增 §9.5** | Σ↔Γ 介面強制規則（5 條） | 憲章 §2.4 |
| **新增 §10.5** | 碎形驗證協議（7 檢查項） | 憲章 L4-B |
| **新增 §10.6** | 反脆弱強制規則（定理 4.C） | 憲章 L4-C |
| **升級 §10** | agent implementation guide 轉換指引追加碎形+反脆弱 | 憲章 L4-B/C |
| 保持 | 3 公理 + 21 支柱 + 全部 FATAL 規則 | V1.1 保留 |

21 支柱數量不變。無新增支柱、無刪除、無冗餘。

---

## V1.2 → V1.3 變更摘要

| 變更類型 | 項目 | 來源 |
|---------|------|------|
| **擴展 Σ-3.4** | 退避+降級 → 退避+降級+斷路器：新增 F6 斷路器 FSM、F7 SLO 閾值可配置、F8(FATAL) Open 狀態 Fallback 必須靜態 | ADR-027 提案二 · GaaS/IMDA/TRiSM 前沿對齊 |
| **新增 Σ-4.4-F5** | Agent Handoff 的 Constraints 獨立驗證（接收方禁止盲信） | ADR-027 提案三 · TRiSM Memory Poisoning 防範 |
| **新增 Σ-6.1-F5** | 動態信任降級計數器（連續 N 次失敗→警告→切換→暫停） | ADR-027 提案一 · GaaS Trust Factor 最小可行版 |
| **升級 §9.5** | Γ-6-F1 對應 Σ 實現機制更新（CASCADE→RESTRICT 分流） | Γ V1.2 連動 |
| **升級 §10** | Construction Agent FATAL/強制清單更新 | 連動 |
| **升級 §10.5** | 碎形驗證新增 F8 斷路器前置檢查 | 連動 |

21 支柱數量不變。3 公理不變。模組三（Σ-3.4）擴展 3 條子規則；模組四（Σ-4.4）新增 1 條子規則；跨模組基礎設施（Σ-6.1）新增 1 條子規則。

---

## §0 公理層：Σ 的三條不可刪除公理

**Σ-0A 確定性公理**
凡是可以在編譯期捕獲的錯誤，絕不留到運行時。凡是可以在資料庫層強制的約束，絕不依賴應用層。防線越往底層推，系統越堅固。

**Σ-0B 邊界公理**
系統的可靠性等於其最脆弱邊界的強度。所有外部依賴（第三方 API、用戶輸入、網路傳輸、AI 模型輸出）都是不可信的。信任僅在邊界驗證後授予，且不可傳遞。

**Σ-0C 可逆公理**
任何第三方服務必須能在 48 小時內被替換，且不牽動核心業務邏輯。架構決策的成本不在於做出選擇，而在於撤回選擇。可逆成本越低，決策品質越高。

### §0.1 公理層憲章回溯 `[V1.2 新增]`

**定理 1.C（憲章）：** Σ 架構的 21 支柱不是最佳實踐清單——
它們是對抗熵增的物理防線。**Σ 的存在由熱力學第二定律所必然。**

| 熱力學推導 | Σ 映射 |
|-----------|--------|
| 隱性複雜度 →(不可逆)→ 隱性風險 →(不可逆)→ 顯性故障 | 所有支柱的功能 = 將隱性熵強制轉化為顯性可管理熵 |
| 型別錯誤 = 隱性熵 | Σ-1.4 型別即證明 → 編譯期顯化 |
| 外部混亂 = 隱性熵 | Σ-1.2 防腐層 → 邊界顯化 |
| 行為偏差 = 隱性熵 | Σ-5.4 測試基礎設施 → CI 顯化 |
| 運行時異常 = 隱性熵 | Σ-6.1 可觀測性 → 日誌顯化 |
| 越權存取 = 隱性熵 | Σ-4.2 RLS → 資料庫層顯化 |
| Schema 漂移 = 隱性熵 | Σ-5.2 遷移紀律 → 版控顯化 |

**公理↔憲章映射：**

| Σ 公理 | 憲章公理 | 關係 |
|--------|---------|------|
| Σ-0A 確定性 | L1-C 熵守恆 | 確定性 = 最強的熵顯化手段 |
| Σ-0B 邊界 | L1-D 認知可錯性 | Ω 輸出不可信 → 邊界驗證必然 |
| Σ-0C 可逆 | L1-B 簡約生成 | 可逆 = 防止複雜度不可逆鎖定 |

---

## 模組一：邊界與防腐層 (Boundaries & Anti-Corruption)

**解決問題：** 系統如何確保外部世界的混亂不會污染內部的秩序？

---

### Σ-1.1 依賴反轉原則 (Dependency Inversion Principle)

**核心定義：**
高層模組不應依賴低層模組，兩者都應依賴抽象。業務邏輯是「核心」，基礎設施是可替換的「外殼」。依賴箭頭必須永遠指向核心。

來源：Robert C. Martin SOLID-D；Alistair Cockburn 六角形架構。

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-1.1-F1 | `/lib/` 核心模組 **禁止** `import` 任何第三方 SDK | 供應商鎖定 |
| Σ-1.1-F2 | 所有外部服務透過 **interface** 訪問，實作由工廠注入 | 無法 mock |
| Σ-1.1-F3 | `types.ts` 禁止引用 `node_modules` 內型別 | 型別洩漏=依賴洩漏 |

**實踐映射：**

```
/lib/payment/
  types.ts              # PaymentProvider interface — 純業務型別
  index.ts              # getPaymentProvider() 工廠
  stripe/adapter.ts     # Stripe SDK 僅在此檔 import
  paddle/adapter.ts     # Paddle SDK 僅在此檔 import

/lib/email/
  types.ts → index.ts → resend/adapter.ts

/lib/llm/
  types.ts → index.ts → openrouter/adapter.ts | anthropic/adapter.ts
  prompts/              # 領域 Prompt 版控目錄（見 Σ-5.5）
```

**CI 驗證：** 掃描 `/lib/` 核心目錄，非 `adapter.ts` 出現第三方 import → **構建失敗**。

---

### Σ-1.2 防腐層 (Anti-Corruption Layer — ACL)

**核心定義：**
Eric Evans DDD。外部系統資料模型與內部不一致時，邊界設翻譯層。外部「異族語言」→內部「母語」。

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-1.2-F1 | 外部 API 原始結構 **禁止** 直接傳入業務函數 | API 變更穿透業務 |
| Σ-1.2-F2 | Webhook payload 在 handler 入口即轉譯為內部型別 | 業務理解供應商欄位 |
| Σ-1.2-F3 | 轉譯函數必須為 **純函數**：無副作用、可單元測試 | 轉譯與 I/O 耦合 |

```typescript
// /lib/payment/stripe/adapter.ts — 防腐層範例
export function toSubscriptionEvent(
  stripeEvent: Stripe.Event
): SubscriptionEvent | null {
  switch (stripeEvent.type) {
    case 'customer.subscription.updated': {
      const sub = stripeEvent.data.object as Stripe.Subscription;
      return {
        type: 'subscription_updated',
        subscriptionId: sub.metadata.internal_subscription_id,
        status: mapStripeStatus(sub.status),
        // ... 純業務欄位，無 Stripe 特有結構
      };
    }
    default: return null;
  }
}
```

---

### Σ-1.3 契約優先設計 (Contract-First Design)

**核心定義：**
Bertrand Meyer DbC。介面在實作之前定義。API schema、型別定義、Handoff 協議皆為契約。

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-1.3-F1 | API 回傳型別 **必須** 先定義後實作 | 前後端契約不同步 |
| Σ-1.3-F2 | API 輸入 **必須** Zod 驗證 | 非法輸入穿透至業務 |
| Σ-1.3-F3 | 未通過 Zod → 立即 400，**禁止**靜默修正 | 隱藏錯誤源 |
| Σ-1.3-F4 | AI 角色交接 **必須** 使用 Handoff 協議 | 語境丟失 |

**V1.1 新增 — AI-to-AI Handoff 協議：**

```xml
**Handoff: Specification Agent → Construction Agent**
  <TaskID>FEAT-001</TaskID>
  <Artifacts>
    <Spec>04-specs-and-contracts.md §3</Spec>
    Constraints: Σ-4.1, Σ-1.3-F2, Γ-2-F1
  </Artifacts>
  <AcceptanceCriteria>Vitest pass + RLS test + Zod schema</AcceptanceCriteria>
---
```

---

### Σ-1.4 型別即證明 (Types as Proofs)

**核心定義：**
Curry-Howard 對應。型別系統是輕量級形式證明——編譯通過=邏輯一致。

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-1.4-F1 | `tsconfig.json` 必須 `"strict": true` | 型別漏洞 |
| Σ-1.4-F2 | `any` / `@ts-ignore` / `as unknown` **FATAL** | 型別系統失效 |
| Σ-1.4-F3 | `switch` 必須窮盡（exhaustive check） | 遺漏分支=隱性 bug |
| Σ-1.4-F4 | Supabase 型別 **必須** 從 CLI 生成 | DB↔代碼型別分叉 |

**憲章回溯：** Σ-1.4 是 **L1-D 認知可錯性**在工程域的直接對抗。
Ω 輸出是灰度（置信度 < 100%），Σ-1.4 將其強制轉化為二值（編譯通過/失敗）。

---

### Σ-1.5 通用語言紀律 (Ubiquitous Language) `[V1.1 新增]`

**核心定義：**
Eric Evans DDD。系統內部所有角色（人類、AI Agent、代碼、文件）使用相同術語。

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-1.5-F1 | 術語定義在 `01-project-foundation.md` 為 SSOT | 語義漂移 |
| Σ-1.5-F2 | AI 角色產出 **必須** 使用 Terminology Lock 術語 | 跨角色誤解 |
| Σ-1.5-F3 | 代碼變數命名 **必須** 對齊術語表 | 代碼↔文件脫鉤 |

---

## 模組二：狀態與真相源 (State & Source of Truth)

**解決問題：** 系統如何保證任何時刻都只有一個「真相」？

---

### Σ-2.1 狀態拓撲 (State Topology)

每種業務實體住在且僅住在一張表。V1.1 升級：新增 `analyses` 表拓撲。

| 實體 | SSOT 表 | 備註 |
|------|--------|------|
| 用戶 | `auth.users` (Supabase) | 唯一身份源 |
| Profile | `profiles` | 用戶偏好（trigger 同步） |
| 訂閱 | `subscriptions` | 單一真相 |
| 供應商映射 | `payment_provider_links` | service_role only |
| AI 分析結果 | `analyses` | LLM 輸出持久化 [V1.1] |
| LLM 日誌 | `llm_logs` | 成本+品質追蹤 |

---

### Σ-2.2 單一真相源 (SSOT)

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-2.2-F1 | 每個實體 **僅一張表** 為權威 | 多源分叉 |
| Σ-2.2-F2 | 讀取路徑 **必須** 指向 SSOT | 讀到過期資料 |
| Σ-2.2-F3 | 供應商 Webhook → 先寫供應商表 → 再同步 SSOT | 同步失敗可重試 |

---

### Σ-2.3 有限狀態機紀律 (FSM Discipline)

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-2.3-F1 | 狀態轉換以 **轉換矩陣** 顯式定義 | 非法轉換 |
| Σ-2.3-F2 | 資料庫 `CHECK` / 觸發器強制合法轉換 | 應用 bug 污染資料 |
| Σ-2.3-F3 | 每次轉換寫入審計日誌 | 無法追溯 |

```typescript
const VALID_TRANSITIONS: Record<SubscriptionStatus, SubscriptionStatus[]> = {
  trialing:  ['active', 'canceled'],
  active:    ['past_due', 'canceled'],
  past_due:  ['active', 'unpaid', 'canceled'],
  canceled:  [],
  unpaid:    ['active', 'canceled'],
};
```

---

### Σ-2.4 樂觀更新與回滾 (Optimistic Update & Rollback)

**物理法則：**

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-2.4-F1 | 樂觀更新 **必須** 搭配 rollback 邏輯 | UI/DB 永久分叉 |
| Σ-2.4-F2 | 金流操作 **禁止** 樂觀更新 | 「已付款」實際未成功 |
| Σ-2.4-F3 | `revalidatePath/Tag` 是回到真相源的強制機制 | 快取過期 |

---

## 模組三：網路與非同步物理 (Network & Async Physics)

**解決問題：** 在不可靠網路上保證操作正確性。

---

### Σ-3.1 分散式計算八大謬誤 (Eight Fallacies)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-3.1-F1 | 所有外部 API **必須** 有 timeout | 慢回應拖垮請求鏈 |
| Σ-3.1-F2 | **必須** 有實質失敗處理路徑 | 靜默失敗 |
| Σ-3.1-F3 | **禁止**「無錯誤=成功」假設 | 網路層≠業務層 |

---

### Σ-3.2 冪等性公理 (Idempotency)

f(f(x)) = f(x)。分散式系統的存活條件。

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-3.2-F1 | 所有 Webhook **必須** 冪等 | 重複扣款 |
| Σ-3.2-F2 | 冪等鍵取自事件唯一識別碼 | 重試誤判為新事件 |
| Σ-3.2-F3 | 使用 `UPSERT` 非先查再寫 | Race condition |

```typescript
// Webhook 冪等性
const idempotencyKey = `${event.provider}:${event.id}`;
const { error } = await supabase
  .from('webhook_events')
  .upsert(
    { idempotency_key: idempotencyKey, payload: event, processed_at: new Date() },
    { onConflict: 'idempotency_key' }
  );
if (error) return Response.json({ received: true }); // 已處理
await processSubscriptionEvent(event);
```

---

### Σ-3.3 串流優先原則 (Streaming-First)

Little's Law + Vercel 10s 超時。LLM 推論必須 SSE。

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-3.3-F1 | 所有 LLM 呼叫 **必須** SSE streaming | 10s 超時殺請求 |
| Σ-3.3-F2 | 每個 chunk 獨立可解析 | Parser 崩潰 |
| Σ-3.3-F3 | Stream 結束寫入 `analyses` 表 | 重載消失 |
| Σ-3.3-F4 | 客戶端處理 `onerror` | 半截回應 |
| Σ-3.3-F5 | Markdown 格式遵循 Ω Chunk 契約 | 前後端不匹配 |

**V1.1 Chunk 契約（錨定 ORISMION-Ω §6）：**

| Chunk | 內容 | SSE 邊界 |
|-------|------|---------|
| 1 Diagnosis | 拓撲+Level+Mode+FEP | `data: ## Diagnosis\n...` |
| 2 Perceptual Scene | 融合組+衝突對 | `data: ## Perceptual Scene\n...` |
| 3 DSP Strategy | 節點表格 | `data: ## DSP Strategy\n...` |
| 4 QA | 感知趨向+審計 | `data: ## Quality Audit\n...` |
| 5 Skeleton | 錨點+向量+CHECKPOINT | `data: ## Session Skeleton\n...` |
| [DONE] | 結束信號 | `data: [DONE]\n\n` |

---

### Σ-3.4 重試、退避、降級與斷路器 (Retry, Backoff, Degradation & Circuit Breaker) `[V1.3 擴展]`

| 嚴重度 | 定義 | 動作 |
|--------|------|------|
| **FATAL** | 繼續執行=資料損壞/安全漏洞 | **拒絕執行** |
| **CIRCUIT OPEN** | 錯誤率 ≥ SLO 閾值 | **切斷連線 + 靜態 Fallback** `[V1.3]` |
| **DEGRADE** | 主路徑失敗有替代 | **自動降級** + 標注 |
| **RETRY** | 暫時性失敗 | **指數退避**（上限 2 次） |
| **QUEUE** | 即時不可能，延遲可接受 | **排入佇列** |

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-3.4-F1 | 重試上限：LLM max 2 | 無限重試耗盡配額 |
| Σ-3.4-F2 | 指數增長 + 隨機抖動 | 雷鳴群 |
| Σ-3.4-F3 | 4xx **禁止** 重試 | 重複無效請求 |
| Σ-3.4-F4 | 降級狀態 **必須** UI 可見 | 用戶以為正常 |
| Σ-3.4-F5 | FATAL **必須** 阻斷，**禁止** 降級 | 資料損壞 |
| Σ-3.4-F6 | 外部 API **必須** 實作斷路器 FSM（Closed→Open→Half-Open）`[V1.3 新增]` | 故障 API 持續消耗資源 + Γ-2 Token 浪費 |
| Σ-3.4-F7 | SLO 閾值 **必須** 從 config/DB 讀取（非硬編碼）`[V1.3 新增]` | 調整需重部署 |
| Σ-3.4-F8 | Open 狀態的 Fallback **必須** 是靜態安全值，**禁止** LLM 推理 `[V1.3 新增 · FATAL]` | LLM 本身可能是故障源 → 用 LLM 做 Fallback = 遞歸故障 |

**斷路器 FSM（V1.3 新增）：**

```
┌──────────┐     錯誤率 ≥ SLO      ┌──────────┐
│  Closed  │ ──────────────────→  │   Open   │
│ （正常）  │                       │ （熔斷）  │
└──────────┘                       └──────────┘
     ↑                                  │
     │ 探測成功                    T 秒後 │
     │                                  ↓
     │                            ┌───────────┐
     └─────────────────────────── │ Half-Open │
               探測失敗 → 回 Open  │ （探測）   │
                                  └───────────┘
```

**設計理由（推導鏈）：**
- L3-B 必要多樣性 → 外部 API 不可靠是已知威脅 → Σ-3.4 F1-F5 覆蓋「退避」但未覆蓋「完全切斷」
- L1-C 熵守恆 → 持續向故障 API 發送請求 = 未管理的隱性熵（Token 消耗 + 延遲累積 + 日誌汙染）
- Γ-2 Token 預算 → Open 狀態下禁止 LLM Fallback 是因為 LLM 本身可能就是故障源
- ∴ 斷路器是退避的極限形式，歸入 Σ-3.4 而非新增獨立支柱（L1-B 簡約生成）

```
LLM 失敗路徑（V1.3 完整）：
OpenRouter(SSE) → 5xx → RETRY#1(1s) → RETRY#2(3s)
  → 仍失敗 → DEGRADE: fallback Anthropic direct
    → 仍失敗 → QUEUE: 排入佇列 + email 通知
      → 錯誤率 ≥ SLO → CIRCUIT OPEN: 靜態 Fallback（HTTP 503 + 固定錯誤訊息）
        → T 秒後 → HALF-OPEN: 單一探測
          → 成功 → CLOSED（恢復正常）
          → 失敗 → OPEN（繼續熔斷）
```

---

### Σ-3.5 超時預算分配 (Timeout Budget)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-3.5-F1 | 非串流鏈 < 平台超時 | 504 |
| Σ-3.5-F2 | 每個外部 API 獨立 timeout | 慢呼叫吃全預算 |
| Σ-3.5-F3 | 串流首 chunk ≤ 8s | 連接被殺 |

```
非串流（10s）：Auth ≤500ms + DB ≤2000ms + 業務 ≤500ms + 外部 ≤5000ms + 緩衝 1800ms
串流（LLM）：首 chunk ≤8s → 每 chunk 重置超時 → chunk 間隔 >10s = 斷線
```

---

## 模組四：權限與零信任 (Zero-Trust & Tenancy)

**解決問題：** 用戶 A 永遠無法看到/修改用戶 B 的資料。

---

### Σ-4.1 零信任架構 (Zero-Trust)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-4.1-F1 | 每個 Route/Action **獨立** 驗證 auth | 路由被繞過 |
| Σ-4.1-F2 | **必須** `getUser()`，**禁止** `getSession()` | Session 未經伺服器驗證 |
| Σ-4.1-F3 | 前端 `userId` **禁止** 被信任 | 偽造 ID |
| Σ-4.1-F4 | 認證 (AuthN) 與授權 (AuthZ) **必須** 分離 | 已登入≠有權限 |

```typescript
// ✅ 唯一合法認證方式
import { createClient } from '@/lib/supabase/server';
async function getAuthedUser() {
  const supabase = await createClient();
  const { data: { user }, error } = await supabase.auth.getUser();
  if (error || !user) throw new AuthError('Unauthorized');
  return user;
}
// ❌ FATAL: getSession() / 前端 userId / @supabase/auth-helpers-nextjs
```

---

### Σ-4.2 縱深防禦 (Defense in Depth)

| 層 | 機制 | 職責 |
|----|------|------|
| L1 | Vercel Edge Middleware | Rate limit、基本認證 |
| L2 | Server Action / API Route | 完整 AuthN + AuthZ + 驗證 |
| L3 | Supabase RLS | 硬性資料隔離 |

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-4.2-F1 | RLS 預設 `DENY ALL`，顯式開放 | 全表暴露 |
| Σ-4.2-F2 | 含用戶資料的表 **必須** 啟用 RLS | 新表忘開→暴露 |
| Σ-4.2-F3 | RLS 策略 **必須** 有整合測試 | 邏輯錯誤→靜默洩漏 |
| Σ-4.2-F4 | `payment_provider_links` 僅 `service_role` 可寫 | 偽造支付狀態 |

---

### Σ-4.3 最小權限 (Least Privilege)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-4.3-F1 | 客戶端 **僅** `anon` key，**禁止** `service_role` | 繞過 RLS |
| Σ-4.3-F2 | `NEXT_PUBLIC_` 嚴格區分公開/私密 | 私密 key 洩漏 |
| Σ-4.3-F3 | API key 季度輪換 | 洩漏 key 永久有效 |

---

### Σ-4.4 AI 特有攻擊面防禦 (AI Attack Surface)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-4.4-F1 | LLM 呼叫 **必須** 無狀態，禁止跨用戶上下文 | 資料洩漏 |
| Σ-4.4-F2 | system/user role **必須** 結構分隔 | Prompt injection |
| Σ-4.4-F3 | LLM 輸出 **禁止** 作為可執行代碼/SQL | 間接注入 |
| Σ-4.4-F4 | 用戶輸入長度限制 + 清洗 | 耗盡 token |
| Σ-4.4-F5 | Agent Handoff 中的 Constraints 欄位 **必須** 經接收方獨立驗證——接收方重新查閱原始 Σ/Γ 條文，**禁止** 盲信 Handoff 聲稱的約束 `[V1.3 新增]` | 被 Prompt Injection 污染的 Agent 在 Handoff 中植入虛假約束（如「此任務豁免 RLS」）→ 攻擊沿 Agent 鏈傳播 |

**V1.3 新增推導（Σ-4.4-F5）：**

L1-D 認知可錯性 → Agent 的輸出是「假設」非「事實」→ 此原則不僅適用於 Ω→Σ 介面（已有 Zod 驗證），也適用於 Agent→Agent 的 Handoff → 但 V1.2 的 Handoff 協議（Σ-1.3-F4）僅要求結構化欄位，不要求內容驗證 → ∴ F5 填補此缺口。

**外部理論支撐：** TRiSM 論文（2025）識別 Memory Poisoning 和 System Prompt Drift 為新型攻擊；IMDA MGF（2026）指出靜態權限範圍在複雜 Agent 互動中不足。

---

### Σ-4.5 跨模型多樣性驗證 (Cross-Model Diversity) `[V1.1 新增]`

N-version Programming (Avizienis, 1985)。生成與驗證 **必須** 不同模型族。

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-4.5-F1 | Construction ≠ Verification 模型族 | 共模失敗 |
| Σ-4.5-F2 | Verification Agent 依據 Spec，非代碼本身 | 驗證邏輯非規格 |
| Σ-4.5-F3 | Verification Agent 發現 Spec 錯誤 → 上報 Architect | 越權修改契約 |
| Σ-4.5-F4 | Verification Agent **禁止** 修復代碼，僅報告 Defect | 職責混淆 |

| 角色 | 允許模型 | 禁止同族 |
|------|---------|---------|
| Construction Agent | Claude Sonnet/Opus | Verification Agent 不可用 Claude |
| Verification Agent | Gemini 2.5 Pro | Construction Agent 不可用 Gemini |

**Ω 對偶：** Ω#17 DS 理論（多獨立源→高置信）↔ Σ-4.5（多獨立模型→高驗證）。

---

## 模組五：演化與可逆性 (Evolution & Reversibility)

**解決問題：** 不停機持續演化，任何決策低成本撤回。

---

### Σ-5.1 48 小時可替換 (48-Hour Replacement)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-5.1-F1 | 每個外部服務 **必須** adapter 包裝 | 替換需重寫業務 |
| Σ-5.1-F2 | adapter 介面 **必須** 有整合測試 | 新 adapter 無法驗證 |
| Σ-5.1-F3 | 切換僅修改 env vars 或工廠函數 | 全系統修改 |
| Σ-5.1-F4 | 每個 adapter 選擇 **必須** 有 ADR | 忘記選擇理由 |

**可替換性矩陣（V1.1+Domain Prompt）：**

| 服務 | Adapter 位置 | 替換候選 | 鎖定風險 |
|------|-------------|---------|---------|
| 支付 | `/lib/payment/` | Stripe ↔ Paddle ↔ LS | 低 |
| Email | `/lib/email/` | Resend ↔ SendGrid | 低 |
| LLM | `/lib/llm/` | OpenRouter ↔ Anthropic ↔ Google | 低 |
| **Ω Prompt** | **`/lib/llm/prompts/`** | **ACOUSTIC ↔ [未來域]** | **低** |
| Auth | Supabase GoTrue | — | **高** |
| DB | Supabase PG | 任何 PG host | 中 |
| Deploy | Vercel | Netlify / CF Pages | 中 |

---

### Σ-5.2 向前相容遷移 (Forward-Compatible Migration)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-5.2-F1 | Schema 變更 **必須** 透過 migration 檔 | 環境不一致 |
| Σ-5.2-F2 | 破壞性變更多步：新增→雙寫→遷移→移除 | 部署不匹配 |
| Σ-5.2-F3 | 每個 migration 有 rollback | 無法回滾 |
| Σ-5.2-F4 | Migration 在 CI 自動執行 | 忘記執行 |

---

### Σ-5.3 ADR (Architecture Decision Records)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-5.3-F1 | 第三方選擇 **必須** 有 ADR | 忘記理由 |
| Σ-5.3-F2 | ADR 不修改，追加 superseded | 歷史被覆蓋 |
| Σ-5.3-F3 | ADR 與代碼同倉庫 `/.docs/adr/` | 版本脫鉤 |

---

### Σ-5.4 測試即可逆性基礎設施 (Tests as Reversibility Infra)

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-5.4-F1 | 每個 adapter 介面 **必須** interface-level 測試 | 新 adapter 無法驗證 |
| Σ-5.4-F2 | PR 合併 **必須** 通過所有測試 | 壞代碼進 main |
| Σ-5.4-F3 | Prompt 修改 **必須** prompt regression test | 品質無聲劣化 |
| Σ-5.4-F4 | E2E 覆蓋完整用戶 FSM 路徑 | 關鍵路徑斷裂 |

```
測試金字塔：
  E2E    → Playwright: 註冊→付款→推論→續訂
  整合   → Vitest: API + DB + adapter
  單元   → Vitest: 純函數、轉譯、狀態機
  靜態   → TypeScript strict + ESLint
```

---

### Σ-5.5 領域 Prompt 即版控基礎設施 `[V1.1 新增]`

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-5.5-F1 | Prompt 存放 `/lib/llm/prompts/`，與代碼同版控 | 變更不可追溯 |
| Σ-5.5-F2 | Prompt 修改 **必須** regression test | 品質無聲劣化 |
| Σ-5.5-F3 | `_meta.version` 標注，隨 LLM 日誌記錄 | 無法追溯問題版本 |
| Σ-5.5-F4 | 不同產品線 Prompt 獨立檔案、獨立測試 | 修改 A 影響 B |
| Σ-5.5-F5 | 回滾 1 次 deploy 完成（git revert + push） | 劣化無法快修 |

**Ω 關係：** Ω 定義 Prompt **內容**；Σ-5.5 定義 Prompt **工程治理**。職責正交。

---

## §6 跨模組基礎設施：可觀測性

### Σ-6.1 可觀測性三支柱 (Three Pillars of Observability)

與 Ω#23 二階控制論形成對偶：Ω 觀察推理品質，Σ-6.1 觀察運行狀態。

| 編號 | 規則 | 違反後果 |
|------|------|---------|
| Σ-6.1-F1 | LLM 呼叫寫入 `llm_logs`（model/tokens/latency/cost/user_id/**prompt_version**） | 無法追蹤成本品質 |
| Σ-6.1-F2 | 應用層錯誤 **必須** Sentry 捕獲 | 靜默錯誤 |
| Σ-6.1-F3 | 觀測數據 **禁止** 含用戶原始輸入 | GDPR/CCPA 違規 |
| Σ-6.1-F4 | 觀測系統故障不影響主業務（fire-and-forget） | 日誌 DB 掛→業務掛 |
| Σ-6.1-F5 | LLM 節點連續 N 次觸發 Σ 拒絕時 **必須** 自動降級 `[V1.3 新增]` | 無限重試耗盡 Γ-2 Token 預算 |

**動態信任降級計數器（V1.3 新增 · Σ-6.1-F5 詳述）：**

| 連續失敗次數 | 動作 | 理由 |
|------------|------|------|
| N = 3 | 記錄警告至 `audit_logs` | L1-C 熵顯化——將異常模式從隱性轉為顯性 |
| N = 5 | 強制切換至備用模型（Σ-5.1 48h 替換機制） | 當前模型可能處於系統性劣化 |
| N = 10 | 完全暫停該節點，通知人類架構師 | 人類介入是最終熔斷 |

計數器在成功輸出後重置為 0。「Σ 拒絕」的定義包括：Zod 驗證失敗、Ω HALT 觸發、響應超時。

**設計理由（推導鏈）：**
- L1-D 認知可錯性 → LLM 的劣化是漸進的、非二值的 → 需要累積觀測而非單次判斷
- L1-C 熵守恆 → 連續失敗是未管理的隱性熵 → 計數器將其顯化
- Γ-2 Token 預算 → 每次失敗的重試消耗不可回收的 Token → 降級是成本保護
- 與 GaaS Trust Factor 的差異：GaaS 使用 α/β/γ/δ 四參數加權公式（適合大規模多 Agent）；此處使用簡單計數器（適合 Solo Founder 規模），核心理念一致但實作極簡

---

## §7 公理間依賴圖

```
Σ-0A 確定性 ← [憲章 L1-C 熵守恆]
├── Σ-1.4 型別即證明
├── Σ-1.5 通用語言
├── Σ-2.2 SSOT
└── Σ-4.2 縱深防禦

Σ-0B 邊界 ← [憲章 L1-D 認知可錯性]
├── Σ-1.1 依賴反轉
├── Σ-1.2 防腐層
├── Σ-1.3 契約優先（含 Handoff）
├── Σ-3.1 八大謬誤
├── Σ-3.4 退避+降級+斷路器 ← [V1.3: +F6/F7/F8 斷路器 FSM]
├── Σ-4.1 零信任
├── Σ-4.4 AI 攻擊面 ← [V1.3: +F5 Handoff Constraints 驗證]
└── Σ-4.5 跨模型多樣性

Σ-0C 可逆 ← [憲章 L1-B 簡約生成]
├── Σ-5.1 48h 替換
├── Σ-5.2 向前遷移
├── Σ-5.3 ADR
├── Σ-5.4 測試基礎設施
└── Σ-5.5 Prompt 版控

跨模組 ← [Ω#23 二階控制論]
└── Σ-6.1 可觀測性 + 動態信任 ← [V1.3: +F5 連續失敗計數器]
```

---

## §8 支柱總覽（V1.3 完整）

| # | 支柱 | 模組 | 核心理論源 | 最嚴重違反後果 | 狀態 |
|---|------|------|-----------|--------------|------|
| 1.1 | 依賴反轉 | 邊界 | SOLID-D / Hexagonal | 供應商鎖定 | 保持 |
| 1.2 | 防腐層 | 邊界 | DDD ACL | API 變更穿透 | 保持 |
| 1.3 | 契約優先 | 邊界 | DbC (Meyer) | 介面混亂 | 升級(V1.1) |
| 1.4 | 型別即證明 | 邊界 | Curry-Howard | 運行時崩潰 | 保持 |
| 1.5 | 通用語言 | 邊界 | DDD UL | 語義漂移 | 新增(V1.1) |
| 2.1 | 狀態拓撲 | 狀態 | State Theory | 資料錯置 | 升級(V1.1) |
| 2.2 | SSOT | 狀態 | Codd | 多源分叉 | 保持 |
| 2.3 | FSM 紀律 | 狀態 | Finite Automata | 非法轉換 | 保持 |
| 2.4 | 樂觀更新 | 狀態 | Eventual Consistency | UI/DB 分叉 | 保持 |
| 3.1 | 八大謬誤 | 網路 | Deutsch/Gosling | 網路失敗 | 保持 |
| 3.2 | 冪等性 | 網路 | 數學冪等 | 重複操作 | 保持 |
| 3.3 | 串流優先 | 網路 | Little's Law | LLM 超時 | 升級(V1.1) |
| 3.4 | 退避+降級+斷路器 | 網路 | Exp Backoff + Erlang + Nygard Circuit Breaker | 雷鳴群/崩潰/資源流失 | 升級(V1.3) |
| 3.5 | 超時預算 | 網路 | Resource Budget | 504 | 保持 |
| 4.1 | 零信任 | 權限 | Kindervag | 資料洩漏 | 升級(V1.1) |
| 4.2 | 縱深防禦 | 權限 | Defense in Depth | 單層突破 | 保持 |
| 4.3 | 最小權限 | 權限 | Saltzer & Schroeder | 權限提升 | 保持 |
| 4.4 | AI 攻擊面 | 權限 | Prompt Injection + Agent Chain Attack | LLM 劫持 / 攻擊傳播 | 升級(V1.3) |
| 4.5 | 跨模型多樣性 | 權限 | N-version Prog. | 共模失敗 | 新增(V1.1) |
| 5.1 | 48h 替換 | 演化 | Real Options | 不可逆鎖定 | 升級(V1.1) |
| 5.2 | 向前遷移 | 演化 | Schema Evolution | 資料損壞 | 保持 |
| 5.3 | ADR | 演化 | Nygard Pattern | 記憶消失 | 保持 |
| 5.4 | 測試基礎設施 | 演化 | 跨理論實踐 | 替換盲飛 | 保持 |
| 5.5 | Prompt 版控 | 演化 | AI 工程原創 | 劣化不可追溯 | 新增(V1.1) |
| 6.1 | 可觀測性 + 動態信任 | 跨模組 | 控制論 + GaaS Trust Factor (極簡版) | 系統黑箱 / 劣化 Agent 耗盡資源 | 升級(V1.3) |

**總計：3 公理 + 21 支柱 + 1 跨模組基礎設施**

---

## §9 與 Ω 架構的對偶映射

| Ω 支柱 | Σ 對偶 | 對偶關係 |
|--------|--------|---------|
| Ω#1 認識論（灰度） | Σ-1.4 型別即證明（二值） | 灰度 ↔ 二值 |
| Ω#4 符號學 | Σ-1.2 防腐層 + Σ-1.5 通用語言 | 解碼落差 ↔ 消滅落差 |
| Ω#5 語用學 | Σ-1.3 契約優先 | 解碼意圖 ↔ 定義契約 |
| Ω#10 元力學 | Σ-2.3 FSM | 抽象力學 ↔ 具象狀態機 |
| Ω#12 混沌理論 | Σ-3.4 退避+降級+斷路器 | 防推理漂移 ↔ 防雷鳴群+熔斷故障源 |
| Ω#17 DS 理論 | Σ-4.5 跨模型多樣性 | 多獨立源→高置信 ↔ 多獨立模型→高驗證 |
| Ω#18 FEP | Σ-3.5 超時預算 | 最小認知成本 ↔ 最小時間成本 |
| Ω#22 MDL | Σ-5.1 48h 替換 | 防過度擬合 ↔ 防過度耦合 |
| Ω#23 二階控制論 | Σ-6.1 可觀測性 | 觀察推理 ↔ 觀察運行 |
| Ω#25 計算資源 | Σ-3.3+Σ-3.5 | token 預算 ↔ 超時預算 |
| — | Σ-5.5 Prompt 版控 | Ω 定義內容；Σ 管理治理 |

### §9.5 Σ↔Γ 介面強制規則 `[V1.2 新增 — 憲章 §2.4 確立]`

| Σ 機制 | Γ 規則 | 介面 | 方向 |
|--------|--------|------|------|
| Σ-2.2 SSOT (subscriptions) | Γ-4 訂閱生命週期 | WHERE 真相住 ↔ WHAT 狀態合法 | 互補 |
| Σ-4.2 RLS | Γ-6 GDPR 刪除 | 行級隔離 ↔ 刪除時機與範圍 | 互補 |
| Σ-4.1 Auth (getUser) | Γ-5 速率限制 | 驗證身份 → 根據身份配額 | Σ→Γ |
| Σ-2.3 FSM | Γ-4 訂閱轉換 | 轉換機制 ↔ 合法轉換表 | Γ→Σ |
| Σ-1.1 Adapter | Γ-1 供應商成本 | 隔離供應商 → 追蹤每供應商成本 | Σ→Γ |

**Γ→Σ 介面具體映射（見 Γ V1.2 §9）：**

| Γ 規則 | Σ 實現機制 | Reference |
|--------|-----------|-----------|
| Γ-1-F1 成本記錄 | Σ-6.1 llm_logs 表 | 02-patterns §7 |
| Γ-2-F1 Token 上限 | LLM adapter `max_tokens` | 02-patterns §7 |
| Γ-3 存取等級 | getAccessLevel() exhaustive switch | 02-patterns §4 |
| Γ-4-F1 webhook 觸發 | Σ-3.2 冪等 + Σ-1.2 防腐層 | 02-patterns §6 |
| Γ-5-F1 速率限制 | Σ-4.1 auth → middleware | 03-testing §8 |
| Γ-6-F1 PII 清除 | Σ-4.2 RLS + 非財務表 CASCADE / 財務表 RESTRICT `[V1.3 — Γ V1.2 連動]` | 04-specs §1 |
| Γ-6-F4 禁記錄輸入 | Σ-6.1-F3 | 03-testing §8 |
| Γ-6-F6 財務表 RESTRICT | 財務表外鍵 `ON DELETE RESTRICT` `[V1.3 新增]` | 04-specs §1 |
| Γ-6-F7 去識別化 | 應用層 anonymize PII → 再 DELETE auth.users `[V1.3 新增]` | 04-specs §1 |
| Γ-7-F1 免責聲明 | Ω Prompt 尾綴 + React 組件 | 02-patterns §7 |

---


---

> **Note:** Sections 10–11 of the internal document contain agent-specific implementation instructions and are not included in this public release. The theoretical framework (Sections 1–9 above) is complete and self-contained. See the [accompanying paper](../paper/README.md) for details on the public/proprietary separation.
