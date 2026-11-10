# ADR-0005: Provide a robotics-centric Hardware Catalog

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; Silicon Planning; Platform Architecture
- **Related ADRs:** [0001](0001-unified-end-to-end-robotics-physical-ai-suite.md), [0003](0003-consolidate-compute-one-robot-one-soc.md), [0008](0008-blueprint-first-benchmarking.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 5 (Requirement 1)

## Context and Problem Statement

Today Intel silicon is marketed by product family and market segment rather than
by robot type, and specifications are written for PC buyers (TOPS, clock speeds)
rather than robotics engineers. These specifications do not predict control-loop
jitter, VLA latency, or camera capacity, so platform selection takes weeks and
biases buyers toward competitors with simpler stories.

The platform needs an authoritative, robotics-centric view of every Intel SoC
relevant to robotics whose single job is to answer: *"Which Intel platform is best
suited for my robotics application, and why?"*

## Decision Drivers

- Platform selection must be fast, transparent, and evidence-based.
- Robotics-relevant attributes (determinism, sensor I/O, AI latency, perf/watt, safety) must be first-class.
- Recommendations must be traceable to validated results, not marketing claims.
- Coverage must span shipping products plus disclosed roadmap for multi-year programs.

## Considered Options

1. **Reuse existing PC-oriented product pages** — keep TOPS/clock-centric specs.
2. **Add a robotics landing page** over existing specs without a new attribute model.
3. **Build a robotics-centric Hardware Catalog** with a standardized attribute
   model, platform tiers, and recommendations grounded in blueprint validation.

## Decision Outcome

Chosen option: **Build a robotics-centric Hardware Catalog.** It (a) describes
hardware in terms that matter to robotics engineers, (b) consumes validated
blueprint results from ADR-0008, and (c) translates them into transparent,
objective recommendations by use case. It does **not** define separate benchmark
workloads.

**Coverage:** all currently shipping robotics-relevant Intel products plus
disclosed roadmap, grouped by family (Core Ultra, Core, Atom, dGPU/Arc, Xeon,
connectivity/companion devices, roadmap platforms). SKU lists live in the catalog
and are owned by the respective product lines.

**Robotics-centric attribute model** (generic PC specs remain secondary):
heterogeneous AI compute; measured AI latency; real-time determinism; memory;
sensor and camera I/O; industrial and robot I/O; power and thermals; safety and
security; ruggedness and lifecycle.

**Platform tiering** (recalculated when a relevant blueprint, configuration, or
release changes):

| Tier | Definition |
| ---- | ---------- |
| **T1 — Real-Time Control** | Meets real-time control acceptance criteria of supported arm/mobile blueprints; light AI; low power; industrial. |
| **T2 — Entry Intelligent Robot** | Passes entry configurations of AMR and service-robot blueprints; AI-assisted perception; fanless. |
| **T3 — Consolidated Robot Brain** | Passes AMR, stationary-arm, and mobile-manipulator blueprints with concurrent real-time control. |
| **T4 — Embodied AI Flagship** | Passes the humanoid blueprint with multi-camera perception, whole-body control, and validated Physical AI models in partitioned domains. |
| **T5 — Accelerated Edge AI** | CPU plus discrete Intel Arc GPU; large-model serving and multi-robot inference. |
| **T6 — Infrastructure** | Xeon-class compute for simulation, training, and fleet orchestration. |

**Recommendation dependency:** every recommendation, tier, fit statement, and
performance claim must reference a versioned blueprint validation result and show
the blueprint version, validated configuration, result date, and evidence source.
No robotics suitability claim is published without this traceability.

### Consequences

**Positive**

- Fast, transparent, robotics-relevant platform selection with objective recommendations.
- Tiers and claims are reproducible and auditable against blueprint evidence.
- Lifecycle/roadmap data supports multi-year industrial programs.

**Negative / Trade-offs**

- The catalog cannot publish claims faster than blueprint validation produces them.
- Requires coordination with product lines to keep SKU lists and roadmap current.
- Tier membership must be recomputed on every relevant blueprint/config/release change.

## More Information

- Depends entirely on ADR-0008 for validated results; it defines no workloads itself.
- Tiers T3–T5 operationalize the consolidation policy in ADR-0003.
