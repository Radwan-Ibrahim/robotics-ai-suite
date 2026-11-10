# Architecture Decision Records — Intel Robotics & Physical AI Suite

This directory captures the architecturally significant decisions behind the
Intel Robotics & Physical AI Suite. The records are derived from the
*Robotics AI Suite PRD* (Draft v0.1, October 2026) and restructured as
[Architecture Decision Records (ADRs)](https://adr.github.io/) so each decision
can be reviewed, versioned, and superseded independently.

## What is an ADR?

An ADR documents a single architectural decision: the context that forced the
decision, the options considered, the decision itself, and its consequences.
ADRs are immutable once accepted — a changed decision is captured by a new ADR
that supersedes the old one.

## Status values

- **Proposed** — under review, not yet agreed.
- **Accepted** — agreed and in effect.
- **Superseded** — replaced by a later ADR (linked).
- **Deprecated** — no longer relevant.

All ADRs below are currently **Proposed** pending leadership and architecture review.

## Index

| ADR | Title | Status |
| --- | ----- | ------ |
| [0000](0000-template.md) | ADR template | — |
| [0001](0001-unified-end-to-end-robotics-physical-ai-suite.md) | Adopt a unified, end-to-end Robotics & Physical AI Suite | Proposed |
| [0002](0002-five-layer-platform-architecture.md) | Organize the platform as five software layers on Intel hardware | Proposed |
| [0003](0003-consolidate-compute-one-robot-one-soc.md) | Consolidate compute: one robot, one SoC where possible | Proposed |
| [0004](0004-open-and-upstream-by-default.md) | Open and upstream by default | Proposed |
| [0005](0005-robotics-centric-hardware-catalog.md) | Provide a robotics-centric Hardware Catalog | Proposed |
| [0006](0006-development-kit-catalog.md) | Provide a Development Kit Catalog of reference designs | Proposed |
| [0007](0007-edge-pack-enablement.md) | Use Intel Edge Pack as the enablement and delivery path | Proposed |
| [0008](0008-blueprint-first-benchmarking.md) | Make robotics blueprints the single source of benchmark truth | Proposed |
| [0009](0009-real-time-robotics-control.md) | Enable real-time control through upstream EtherCAT/CAN-FD work | Proposed |
| [0010](0010-physical-ai-model-enablement.md) | Consolidate Physical AI model enablement around upstream-first | Proposed |
| [0011](0011-evolve-geti-into-edge-vision-ai-stack.md) | Evolve Geti into the Intel Edge Vision AI Stack | Proposed |
| [0012](0012-evolve-physical-ai-framework-into-robot-runtime.md) | Evolve the OpenVINO Physical AI Framework into a System 1 / System 2 RobotRuntime | Proposed |

## Traceability to the PRD

| PRD section | Primary ADR(s) |
| ----------- | -------------- |
| 3. Product Vision | 0001 |
| 4. Platform Architecture | 0002, 0003, 0004 |
| 5. Requirement 1: Hardware Catalog | 0005 |
| 6. Requirement 2: Development Kit Catalog | 0006 |
| 7. Requirement 3: Edge Pack Enablement | 0007 |
| 8. Requirement 4: Robotics Blueprints & Benchmarking | 0008 |
| 9. Requirement 5: Real-Time Robotics Control | 0009 |
| 10. Requirement 6: Physical AI Model Enablement | 0010 |
| 11. Requirement 7: Evolve Geti into Edge Vision AI Stack | 0011 |
| 4 & 10. Physical AI Framework → RobotRuntime (extension) | 0012 |
