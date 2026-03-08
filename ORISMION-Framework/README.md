# ORISMION

**Axiomatic Governance for Agentic AI**

ORISMION is a five-layer governance framework for agentic AI systems that derives every rule from a single objective function through explicit inference chains. Unlike prescriptive frameworks that enumerate best practices, ORISMION provides formal justification for *why* each governance rule exists — grounded in thermodynamics, control theory, and epistemology.

---

## Overview

Agentic AI systems — capable of autonomous planning, reasoning, and execution — require governance frameworks that go beyond checklists. ORISMION addresses this by deriving all governance constraints from a single axiom: **survival maximization** (Meta-Telos).

From this objective function, the framework formally derives three irreducible architectural dimensions:

| Dimension | Symbol | Governs | Determinism |
|-----------|--------|---------|-------------|
| Cognition | Ω | How smart is the system? | Non-deterministic |
| Engineering | Σ | How robust is the system? | Deterministic |
| Governance | Γ | How does the system survive? | Policy-adjustable |

Six formal proofs establish that these three dimensions cannot be reduced to one another — they form a **minimal complete basis** for AI system governance. Every downstream rule (33 defense rules, 18 FATAL-level constraints) traces back to the five-layer axiomatic hierarchy (L0–L4) through an explicit derivation chain.

The framework enforces **fractal consistency**: the axiomatic structure is recursively self-similar at the code level, with every API endpoint verified against a mandatory layered ordering (Auth → Circuit Breaker → Governance → Validation → Business Logic → Observability).

## Key Results

- **309** automated tests validating axiomatic compliance in production
- **28** Architecture Decision Records (ADR-000 through ADR-027) documenting every structural decision with its derivation chain
- **33** defense rules across 10 threat classes (requisite variety verified)
- **18** FATAL-level rules (9 Σ + 9 Γ) whose violation blocks code from reaching production
- Framework extensibility validated: integration of 4 frontier frameworks (GaaS, IMDA MGF, TRiSM, HAIG) expanded rules from 28 → 33 without requiring new architectural dimensions

---

## Repository Structure

This repository contains the **theoretical framework** — the public layer of ORISMION as defined in the accompanying paper.

```
ORISMION-Framework/
├── README.md                          # This file
├── LICENSE                            # CC BY-SA 4.0
│
├── constitution/
│   └── 00-grand-unified-theory.md     # The Five-Layer Constitution (L0–L4)
│                                      #   Layer 0: Meta-Telos (survival maximization)
│                                      #   Layer 1: Supreme Axioms (L1-A through L1-D)
│                                      #   Layer 2: Core Triad (Ω-Σ-Γ) + 6 proofs
│                                      #   Layer 3: Cybernetic Dynamics
│                                      #   Layer 4: AI-Native Implementation
│
├── architectures/
│   ├── 01-omega-architecture.md       # Ω Cognition: 25 pillars, 6 modules
│   ├── 02-sigma-architecture.md       # Σ Engineering: 3 axioms, 21 pillars, 9 FATAL rules
│   └── 03-gamma-governance.md         # Γ Governance: 2 axioms, 7 pillars, 9 FATAL rules
│
├── adr/
│   ├── ADR-000-genesis-record.md      # Genesis: how the framework was constructed
│   └── ADR-027-frontier-integration.md # Frontier framework integration decision
│
└── paper/
    └── README.md                      # Links to published paper
```

---

## What This Repository Contains

The **public layer** — everything needed to understand, evaluate, and independently verify the theoretical contribution:

- Complete axiomatic derivations (L0 through L4)
- Six irreducibility proofs establishing the Ω-Σ-Γ basis
- Conflict resolution ordering (Theorem 0.1) with proof sketch
- All pillar definitions with derivation chains
- FATAL rule specifications with violation consequences
- Selected Architecture Decision Records showing the derivation-in-practice methodology

**Language note:** The framework documents are in Mandarin Chinese — the original working language of the production system. They are published as-is to preserve authenticity as primary source materials. The [accompanying paper](paper/README.md) provides the complete theoretical content in English.

## What This Repository Does Not Contain

The **proprietary layer** — implementation-specific materials that concern execution rather than theory:

- Agent prompt content and system instructions
- Handoff protocol field definitions
- Meta-Agent compression gates and FATAL propagation logic
- Reference documents and deployment configurations
- Database schemas and test code
- Specific prompt engineering methodologies

This separation follows the framework's own Principle 2 (L1-B Parsimony): the theoretical contribution is fully verifiable from the public materials; the proprietary materials concern execution, not theory.

---

## Paper

Read the full paper:

> **Axiomatic Governance for Agentic AI: A Five-Layer Constitutional Framework Derived from First Principles and Validated in Production**
>
> Hao-Tse Hsieh (2026)
>
> 📄 [Read on SSRN / arXiv](link_placeholder)

---

## Citation

If you use or reference ORISMION in your work, please cite:

```bibtex
@article{hsieh2026orismion,
  author  = {Hsieh, Hao-Tse},
  title   = {Axiomatic Governance for Agentic {AI}: A Five-Layer Constitutional
             Framework Derived from First Principles and Validated in Production},
  journal = {arXiv preprint},
  year    = {2026}
}
```

---

## License

This work is licensed under [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).

You are free to share and adapt this material for any purpose, including commercial use, provided you give appropriate credit and distribute your contributions under the same license.

---

## Contact

For questions about the theoretical framework, please open an issue in this repository.

For inquiries about ORISMION's production implementation or licensing, contact: research@orismion.com
