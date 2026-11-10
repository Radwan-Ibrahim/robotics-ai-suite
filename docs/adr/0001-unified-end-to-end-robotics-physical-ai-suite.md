# ADR-0001: Adopt a unified, end-to-end Robotics & Physical AI Suite

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; Intel executive leadership; Platform Architecture
- **Related ADRs:** [0002](0002-five-layer-platform-architecture.md), [0005](0005-robotics-centric-hardware-catalog.md), [0006](0006-development-kit-catalog.md), [0008](0008-blueprint-first-benchmarking.md)
- **Source:** Robotics AI Suite PRD v0.1, Sections 1–3

## Context and Problem Statement

Robotics is entering the Physical AI era: robots now combine vision-language
models (VLMs), vision-language-action models (VLAs), world models, and agentic
orchestration with deterministic, safety-critical control. Customers no longer
evaluate a processor in isolation; they evaluate how quickly and reliably a
vendor can help them build, validate, and deploy a complete robot.

Intel already owns most of the required building blocks — heterogeneous CPU/GPU/NPU
SoCs, real-time and time-sensitive networking technologies, AI frameworks,
optimized models, industrial communication support, and reference designs such
as Robinson Bay. These assets are presented today as separate products,
documents, and repositories. Customers must integrate the portfolio themselves
and still cannot answer the basic question: *"Which Intel platform should I build
my robot on, and why?"* This fragmentation biases buyers toward competitors with
simpler, integrated stories and inflates Intel's support burden.

## Decision Drivers

- Customers buy an integrated developer experience, not silicon specifications alone.
- A single question — platform selection with evidence — must have a first-class answer.
- Intel must offer a continuous path from prototype to production without customers leaving the platform.
- Reduce the integration and support burden created by a fragmented portfolio.

## Considered Options

1. **Keep marketing assets separate** (status quo) — continue shipping silicon,
   kits, software, and references as independent products.
2. **Publish a curated catalog only** — add a robotics-facing catalog but leave
   software, kits, and validation unintegrated.
3. **Unify into one end-to-end Suite** — bring silicon, development kits, and the
   robotics software stack together under a single platform with shared
   architecture, catalogs, and validation.

## Decision Outcome

Chosen option: **Unify into one end-to-end Suite.** Intel will define and ship the
**Intel Robotics & Physical AI Suite**, built on three foundational pillars —
Intel SoCs and hardware platforms, Intel development kits and reference designs,
and the Intel Robotics Software Stack — so a customer can arrive with a robot
concept, receive an evidence-based platform recommendation, order a validated
development kit, install a matched software stack in minutes, run a reference
blueprint for their form factor, and follow a documented path to a production
partner system.

### Consequences

**Positive**

- A single, evidence-based answer to "which Intel platform, and why."
- Faster prototyping-to-production and lower integration risk for customers.
- Stronger competitive position against vendors with integrated stacks.
- Reduced Intel support load through validated, reproducible configurations.

**Negative / Trade-offs**

- Requires cross-organization coordination across silicon, software, and ecosystem teams.
- Ongoing ownership for catalogs, validation, and lifecycle management.
- Success depends on the supporting decisions in ADR-0002 through ADR-0011.

## More Information

- Target robotics domains (humanoids, AMRs, arms/cobots, mobile manipulators,
  service, logistics, inspection, medical) are enumerated in PRD §3.2 and shape
  the blueprint portfolio (ADR-0008).
- This ADR sets the strategic frame; subsequent ADRs decide architecture,
  catalogs, enablement, and validation.
