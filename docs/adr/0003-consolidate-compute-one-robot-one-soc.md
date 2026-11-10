# ADR-0003: Consolidate compute — one robot, one SoC where possible

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Platform Architecture; Silicon Planning; Robotics & Physical AI Product Management
- **Related ADRs:** [0002](0002-five-layer-platform-architecture.md), [0005](0005-robotics-centric-hardware-catalog.md), [0008](0008-blueprint-first-benchmarking.md)
- **Source:** Robotics AI Suite PRD v0.1, Sections 2.1 and 4.2

## Context and Problem Statement

Workload consolidation is the dominant architecture trend in robotics. OEMs want
to collapse multi-board designs — a real-time controller, a perception computer,
a safety MCU, and an AI accelerator — onto fewer heterogeneous SoCs, partitioned
by hypervisors or real-time OS domains, to reduce BOM cost, power, cabling, and
integration effort.

Intel's heterogeneous CPU/GPU/NPU SoCs, combined with deterministic computing
(TCC), time-sensitive networking, PREEMPT_RT, and hypervisor partitioning, make
single-SoC consolidation feasible. The platform must take a clear position on how
it leads recommendations: consolidation first, discrete acceleration only when
justified by evidence.

## Decision Drivers

- OEM demand to reduce BOM cost, power, cabling, and integration effort.
- Intel's heterogeneous SoCs can run real-time control, perception, and AI concurrently.
- Determinism must be preserved via partitioning (TCC, PREEMPT_RT, hypervisors, RT OS domains).
- Over-specifying discrete accelerators increases cost and complexity without evidence.

## Considered Options

1. **Multi-board by default** — recommend separate controller, perception, safety, and accelerator boards.
2. **Always single SoC** — force consolidation regardless of workload.
3. **Consolidation-first, evidence-gated discrete acceleration** — lead with a
   single heterogeneous SoC and add discrete acceleration only where blueprint
   evidence shows it is needed.

## Decision Outcome

Chosen option: **Consolidation-first, evidence-gated discrete acceleration.**
The platform leads with consolidation of real-time control, perception, and AI on
a single heterogeneous Intel SoC, using hypervisor or RT-OS partitioning to
preserve determinism. Discrete acceleration (for example an Intel Arc GPU) is
added only where validated blueprint results (ADR-0008) show it is required —
for example large-model serving or multi-robot inference (Hardware Catalog tier
T5, ADR-0005).

### Consequences

**Positive**

- Lower BOM cost, power, cabling, and integration effort for OEMs.
- A differentiated "one robot, one SoC" message grounded in Intel heterogeneous compute.
- Discrete acceleration decisions are justified by measured evidence, not defaults.

**Negative / Trade-offs**

- Requires rigorous partitioning to guarantee determinism alongside AI workloads.
- Some high-end workloads (large VLMs/VLAs, fleet inference) still need discrete GPUs.
- Validation must prove concurrent real-time + perception + AI on a single SoC.

## More Information

- Determinism attributes and partitioning are part of the Hardware Catalog attribute model (ADR-0005).
- Tiers T3/T4 (consolidated brain, embodied-AI flagship) and T5 (accelerated edge) in ADR-0005 operationalize this decision.
