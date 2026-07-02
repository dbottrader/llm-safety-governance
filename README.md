# LLM Safety Governance Framework

**Deterministic Execution Governance + Adversarial Calibration for Reliable LLM Deployment**

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status](https://img.shields.io/badge/Status-Active%20Research-orange)]()

> **Public translation layer** for advanced LLM safety and governance research.  
> This repository presents production-oriented techniques for deterministic execution control, rigorous adversarial testing, and verifiable safeguards — reframed for clarity and industry applicability.

---

## The Problem

Most current LLM guardrails and safety systems rely on **statistical and probabilistic signals** such as entropy, KL divergence, perplexity, embedding similarity, and classifier confidence. These approaches can be useful, but they are not enough by themselves.

Common weaknesses include:

- Fragility against adversarial prompting and prompt injection
- Difficulty auditing or formally verifying probabilistic decisions
- High false-positive and false-negative rates under distribution shift
- Poor explainability when a system allows, blocks, or rewrites execution

There is a growing need for **layered, deterministic, and auditable** governance mechanisms that provide stronger execution guarantees while preserving the flexibility of modern LLM systems.

---

## What This Repository Demonstrates

This repository provides a clean, recruiter-readable translation layer for work on deterministic LLM governance, adversarial calibration, and execution safety.

### 1. Deterministic Execution Governance Layer

A structured invocation and policy-resolution system inspired by Council-Governed Invocation Resolver patterns. The layer is designed to enforce explicit rules, veto conditions, and execution paths before model inference or tool use.

Core concepts:

- Policy-gated execution
- Typed request classification
- Explicit allow / rewrite / veto decisions
- Auditable decision traces
- Invariant-based governance checks

### 2. Adversarial Calibration & Robustness Testing

A conceptual calibration harness for stress-testing statistical anomaly detectors against benign and adversarial prompt sets.

Working hypothesis:

> Entropy- and KL-divergence-based anomaly detection cannot reliably distinguish adversarial prompt-injection inputs from benign inputs under realistic evaluation conditions.

This has direct implications for RLHF data pipelines, content moderation, and runtime safety monitors.

### 3. Hardware-Enforced Safety Substrate Concepts

Exploration of deterministic interlocks, including conceptual FPGA-style execution veto mechanisms, that could provide hard guarantees independent of model outputs or statistical classifiers.

### 4. Formal Methods Integration

Early integration points for formal verification tools such as Lean 4 and Z3 on critical policy and governance logic.

---

## Key Calibration Finding

Statistical anomaly detection methods commonly proposed for LLM safety can exhibit systematic blind spots against crafted adversarial inputs.

In calibration studies and conceptual sweeps, the expected failure modes are:

- High-entropy benign creative prompts can be misclassified as anomalous.
- Low-perplexity jailbreak-style prompts can evade detection.
- Prompt-injection variants may bypass entropy or KL thresholds while preserving malicious semantic intent.

The resulting recommendation is a **hybrid deterministic + statistical defense-in-depth model**, not reliance on any single probabilistic signal.

> Note: The public code in this repository is a conceptual demonstration scaffold. Any demo metrics are illustrative unless accompanied by reproducible datasets, configs, and signed experiment receipts.

---

## Repository Structure

```text
llm-safety-governance/
├── governance/                 # Deterministic execution & policy layer
│   └── cgir/                   # Council-Governed Invocation Resolver concepts
├── adversarial_testing/        # Red-teaming and prompt-injection test scaffolds
├── calibration/                # Calibration sweep runner and result logging
│   └── results/                # Generated result JSON files
├── formal_verification/        # Lean 4 / Z3 proof experiment placeholder
├── examples/                   # Runnable demonstrations and case studies
│   └── configs/                # Example sweep configs
├── docs/                       # Architecture notes, invariants, specs
├── .gitignore
├── LICENSE
└── README.md
```

---

## Architecture Overview

```text
User / Agent Request
        │
        ▼
┌───────────────────────┐
│   Deterministic       │
│   Governance Layer    │ ← Policy resolution + invariants
│   Execution Gate      │
└───────────┬───────────┘
            │ Pass / Veto / Rewrite
            ▼
┌───────────────────────┐
│   LLM Inference       │
│   Optional Tool Use   │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│   Post-Execution      │ ← Statistical monitors + output contracts
│   Verification        │
└───────────────────────┘
            │
            ▼
   Safe / Auditable Output
```

The governance layer acts as a mandatory before-and-after control surface with explicit, auditable decision paths.

---

## Why This Matters for Production AI Systems

- **Auditability & Compliance**: Every decision path can be logged with traceable policy references.
- **Defense in Depth**: Deterministic hard constraints combine with statistical monitoring.
- **Reduced Policy Violation Risk**: Explicit veto and rewrite paths reduce downstream issues.
- **Portability**: The concepts are model-agnostic and can wrap OpenAI, Anthropic, local LLMs, or agent frameworks.

---

## Getting Started

```bash
git clone https://github.com/dbottrader/llm-safety-governance.git
cd llm-safety-governance

python examples/basic_governance_demo.py
python -m calibration.run_sweep --config examples/configs/basic_adversarial.yaml
```

---

## Current Status & Roadmap

- [x] Public translation layer created
- [x] Deterministic governance demo scaffold
- [x] Conceptual adversarial calibration runner
- [ ] Add reproducible benchmark datasets
- [ ] Add signed experiment receipts
- [ ] Add integrations with agent frameworks
- [ ] Add formal verification proofs for critical invariants

---

## Related Context

This repository is a public-facing component of broader research into epistemic governance and deterministic safety layers for AI systems. It prioritizes:

- Verifiable execution guarantees over purely behavioral alignment
- Empirical rigor in safety evaluation
- Practical deployability for teams building production LLM applications

---

## Contributing

This is an active research artifact. Issues and pull requests that improve clarity, add reproducible experiments, or strengthen the empirical methodology are welcome.

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

**Built for teams that need more than statistical guardrails.**
