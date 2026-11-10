# ADR-0008: Make robotics blueprints the single source of benchmark truth

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; Platform Architecture; Blueprint Owners
- **Related ADRs:** [0001](0001-unified-end-to-end-robotics-physical-ai-suite.md), [0005](0005-robotics-centric-hardware-catalog.md), [0006](0006-development-kit-catalog.md), [0010](0010-physical-ai-model-enablement.md), [0011](0011-evolve-geti-into-edge-vision-ai-stack.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 8 (Requirement 4); Section 4.2

## Context and Problem Statement

Recommendations must be credible. If the Hardware Catalog (ADR-0005) relied on
synthetic benchmark workloads that did not correspond to a real customer solution,
claims would diverge from what customers actually experience, and the platform
would maintain two conflicting definitions of "the workload."

The platform needs one solution definition shared by customers, engineering
teams, partners, and the catalogs — grounded in measured results from
customer-facing robotics blueprints rather than marketing specifications or a
separate benchmark suite (the "blueprint-first, not SKU-first" principle).

## Decision Drivers

- Recommendations must reflect real, end-to-end customer solutions.
- Avoid maintaining separate benchmark workloads that do not map to a blueprint.
- Results must be reproducible, versioned, and fully provenanced.
- Partners must be able to submit conformant validation results.

## Considered Options

1. **Separate synthetic benchmark suite** — benchmark SoCs with standalone workloads.
2. **Component micro-benchmarks only** — measure parts (detector, SLAM) in isolation.
3. **Blueprint-first validation** — define customer-facing blueprints and benchmark
   the delivered blueprint end-to-end as the single source of truth.

## Decision Outcome

Chosen option: **Blueprint-first validation.** Requirement 4 defines customer-facing
robotics blueprints and a common validation system used to benchmark them;
separate benchmark workloads that do not correspond to a supported blueprint are
eliminated.

**Supported blueprint portfolio:** AMR; Stationary Robotic Arm; Mobile Manipulator;
Humanoid; Warehouse and Logistics; Service Robot.

**Blueprint definition requirements:** define use case, tasks, system architecture,
supported hardware, sensors, software stack, models, and deployment; provide a
versioned best-known configuration, installation assets, ready-to-run sample code,
and an end-to-end demonstration; declare supported substitutions with limitations;
define measurable acceptance criteria; maintain traceability across versions.

**Benchmarking requirements:** benchmark the delivered blueprint with the same
end-to-end configuration provided to customers; fix and record the full
configuration; measure customer outcomes first (component metrics only for
diagnosis); use realistic sustained power/thermal conditions with concurrent
control/perception/AI; automate and version with full provenance; enable
reproducibility; support partner-submitted results with source and audit status.

**Catalog integration:** produces blueprint validation records, a Hardware Catalog
feed, a Development Kit Catalog feed, and a customer evidence package.

**Governance & success criteria:** a cross-functional owner per blueprint; **no
platform may be recommended for a robotics use case without a current, passing
blueprint validation record**; at least one Intel reference configuration and one
reproducible end-to-end demonstration per blueprint; results published to catalogs
within ten business days of approval; setup-to-first-demo time and end-to-end task
success tracked as primary customer-experience metrics.

### Consequences

**Positive**

- One authoritative solution definition shared across customers, teams, partners, and catalogs.
- Recommendations and tiers are reproducible and auditable (feeds ADR-0005, ADR-0006).
- Eliminates divergence between benchmarks and real customer outcomes.

**Negative / Trade-offs**

- End-to-end blueprint validation is more expensive than synthetic micro-benchmarks.
- Catalog claims are gated on blueprint throughput (publish within ten business days of approval).
- Requires automation, provenance storage, and a partner audit process.

## More Information

- The Hardware Catalog (ADR-0005) and Development Kit Catalog (ADR-0006) consume these feeds.
- Model/pipeline versions referenced by blueprints must align with ADR-0010 and ADR-0011 to avoid conflicting compatibility claims.
