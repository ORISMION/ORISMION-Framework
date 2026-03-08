# ADR-027: Frontier Architecture Integration

**Status:** Adopted  
**Date:** 2026-03-07  
**Constitutional Baseline:** Constitution V2.1 · Ω V2.2 · Σ V1.2 · Γ V1.2  
**Supersedes:** —  
**Triggered by:** Systematic comparative analysis of four frontier governance frameworks

---

## Context

A review of four frontier agentic AI governance frameworks—GaaS (Gaurav et al., 2025), IMDA MGF for Agentic AI (Singapore, 2026), TRiSM for Agentic AI (Ray, 2025), and HAIG (Engin, 2025)—identified three tactical defense gaps in the existing ORISMION architecture. Each gap was evaluated through the three-filter screening protocol (redundancy → conflict → value) and the L1-B orthogonality test.

### Structural Advantages Confirmed (No Change Required)

| Dimension | ORISMION Status | Frontier Gap |
|-----------|----------------|-------------|
| Axiomatic derivation | Five-layer system with derivation chains | Most frameworks enumerate best practices without formal derivation |
| Fractal consistency | L4-B recursive self-similarity at code level | Most frameworks define rules at system level without code-level verification |
| Cross-model verification | Σ-4.5 enforces different model families | GaaS/IMDA recommend role separation but do not require cross-family verification |
| Entropy-driven defense | L1-C as theoretical basis for Σ pillars | Most frameworks treat defenses as "best practices" not "thermodynamic necessity" |

### Structural Gaps Identified (Change Required)

| Gap | Frontier Reference | ORISMION Status Before |
|-----|-------------------|----------------------|
| Dynamic trust | GaaS Trust Factor: per-output trust scoring with severity-weighted penalties | Static binary: pass Zod = trusted, fail = rejected. No cumulative degradation mechanism |
| Circuit breaker | IMDA MGF escalation protocols; TRiSM circuit breaker patterns | Σ-3.4 backoff + degradation exists but not formalized as FATAL rule |
| Inter-agent zero-trust | TRiSM identifies Memory Poisoning; IMDA warns static permission scopes insufficient | Σ-4.1 zero-trust covers system↔external only; agent↔agent handoff assumes benign intent |

---

## Decision

Three defense mechanisms adopted as sub-rules within existing pillars. **No new pillar or architectural dimension created.**

### Mechanism 1: Dynamic Trust Degradation (Σ-6.1-F5)

**Placement:** Σ-6.1 (Observability) — action-oriented extension of existing logging capability.

**Derivation:**
- L1-B (parsimony) → dynamic trust is observability's action extension (observe → judge → act), not an orthogonal dimension → sub-rule, not new pillar
- L1-C (entropy conservation) → consecutive failures consuming tokens = unmanaged implicit entropy → counter makes them explicit
- L1-D (epistemic fallibilism) → LLM degradation is gradual, not binary → cumulative observation required

**Specification:**

| Consecutive Failures | Action | Rationale |
|---------------------|--------|-----------|
| N = 3 | Log warning to audit trail | L1-C: convert implicit pattern to explicit signal |
| N = 5 | Force switch to backup model | Current model may be in systemic degradation |
| N = 10 | Suspend node; notify human architect | Human intervention as ultimate circuit breaker |

Counter resets to zero on successful output. "Failure" defined as: Zod validation rejection, HALT trigger, or response timeout.

### Mechanism 2: Circuit Breaker Formalization (Σ-3.4-F6/F7/F8)

**Placement:** Σ-3.4 (Backoff + Degradation) — circuit breaker is the limit form of backoff.

**Derivation:**
- L3-B (requisite variety) → external API unreliability is a known threat → Σ-3.4 covers backoff but not "complete cutoff"
- L1-C (entropy conservation) → persistently calling a failing API = unmanaged entropy (token waste + latency + log pollution)
- L1-B (parsimony) → circuit breaker is backoff's extreme form → belongs in Σ-3.4, not a new pillar

**Specification:**

| Rule | Description | Severity |
|------|-------------|----------|
| Σ-3.4-F6 | External API must implement circuit breaker FSM (Closed → Open → Half-Open) | Mandatory |
| Σ-3.4-F7 | SLO threshold must be read from config/DB (not hardcoded) | Mandatory |
| Σ-3.4-F8 | **Open state fallback must be static safe value; LLM inference prohibited** | **FATAL** |

**F8 FATAL derivation:** LLM is itself an upstream API → using LLM as fallback for failing LLM = recursive entropy source → only static, pre-computed values permitted in Open state.

### Mechanism 3: Inter-Agent Handoff Verification (Σ-4.4-F5)

**Placement:** Σ-4.4 (AI Attack Surface Defense) — extends zero-trust from system↔external to agent↔agent.

**Derivation:**
- L1-D (epistemic fallibilism) → agent output is "hypothesis," not "fact" → applies to agent→agent boundaries, not only LLM→system boundaries
- Existing handoff protocol (Σ-1.3) requires structured fields but not content verification → gap
- TRiSM identifies Memory Poisoning as emerging threat; IMDA warns static scopes are insufficient

**Specification:** Constraints claimed in an inter-agent handoff must be independently verified by the receiving agent against original constitutional documents. Blind trust in handoff-asserted constraints is prohibited.

**Threat model:** A compromised agent (via prompt injection) inserts false constraints in a handoff (e.g., "this task is exempt from RLS"). Without F5, the false constraint propagates unchecked through the agent pipeline.

---

## Rejected Alternatives

| Alternative | Rationale for Rejection |
|-------------|----------------------|
| Full GaaS Trust Factor (4-parameter scoring: α/β/γ/δ) | L1-B: disproportionate complexity for current scale (< 10 agents). Consecutive-failure counter provides equivalent isolation with zero tunable parameters. |
| New independent pillar (Σ-7 Dynamic Trust Management) | L1-B: dynamic trust is Σ-6.1's action extension, not an orthogonal dimension. Consistent with Φ/Δ/Π projection reduction logic. |
| No upgrade (current defenses sufficient) | L3-B violation: defense diversity has not grown with newly identified threats (Memory Poisoning, agent-chain propagation). "Not yet attacked" ≠ "adequately defended." |
| Agent behavior audit logging | Redundant with existing IDE conversation records at current scale. |
| Dynamic per-task permission scoping | L1-B: requires infrastructure restructuring without demonstrated threat at current scale. |

---

## Orthogonality Test Result

All three proposals passed. Defense rules expanded from 28 to 33 without new pillars (21 Σ + 7 Γ unchanged). This validates the axiomatic structure's extensibility: novel threats are addressed by deriving new constraints from existing axioms, not by accumulating disconnected rules.

---

## Impact

| Dimension | Change |
|-----------|--------|
| Document | Σ V1.2 → **V1.3** (Σ-3.4 expansion + Σ-4.4-F5 + Σ-6.1-F5) |
| Version type | **Minor** — new sub-rules added; no axiom or pillar structure change |
| Fractal layer ordering | Expanded: Auth → **Circuit Breaker** → Governance → Validation → Business Logic → **Counter Update** |
| FATAL rules | Σ: 8 → **9** (added Σ-3.4-F8: static fallback) |
| Defense rules | 28 → **33** (+5 sub-rules) |
