# Architecture Notes

This repository demonstrates a deterministic governance wrapper for LLM and agent execution.

## Core Flow

1. User or agent request enters the governance layer.
2. Request is classified into policy-relevant categories.
3. Deterministic policy rules decide whether to allow, rewrite, or veto execution.
4. Allowed or rewritten requests proceed to model inference or tool use.
5. Post-execution verification checks output contracts and statistical monitors.
6. Decision traces are retained for auditability.

## Design Principle

Statistical monitors are useful, but they should not be the only control surface. A production system should combine:

- deterministic policy gates,
- auditable execution traces,
- statistical anomaly monitoring,
- red-team calibration,
- and formal verification for critical invariants.
