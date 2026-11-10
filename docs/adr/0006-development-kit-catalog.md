# ADR-0006: Provide a Development Kit Catalog of reference designs

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; Ecosystem & Partner Teams; Platform Architecture
- **Related ADRs:** [0001](0001-unified-end-to-end-robotics-physical-ai-suite.md), [0005](0005-robotics-centric-hardware-catalog.md), [0007](0007-edge-pack-enablement.md), [0008](0008-blueprint-first-benchmarking.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 6 (Requirement 2)

## Context and Problem Statement

Customers need readily available robotics systems that meet their compute and I/O
requirements so they can begin development quickly on Intel hardware. Today the
development kit options are fragmented, and it is difficult to identify available
kits, their validation status, and the best fit for a use case.

Intel cannot directly guarantee system availability. Therefore the platform must
define robotics development kit reference designs and work with ecosystem partners
to deliver commercial implementations, documenting them clearly and comprehensively.

## Decision Drivers

- Developers must be able to start prototyping quickly on validated hardware.
- Intel cannot guarantee commercial system availability directly.
- Kits must map cleanly to the Hardware Catalog and blueprints.
- Partners need a simple, open path to contribute commercial systems.

## Considered Options

1. **Point customers to third-party boards** — no Intel reference designs.
2. **Intel-manufactured kits only** — Intel directly builds and sells kits.
3. **Reference designs + partner commercialization** — Intel defines reference
   designs and documents partner commercial implementations in a catalog.

## Decision Outcome

Chosen option: **Reference designs + partner commercialization.** The Suite
provides a **Development Kit Catalog** that:

- Provides a complete specification for every development kit reference design
  (for example, Robinson Bay and Signal Bay), covering the compute board, I/O
  board, system architecture, and design documentation.
- Lists, for each reference design, all partner commercial implementations and
  links to their product and technical documentation.
- Provides a simple contribution process allowing Intel partners to submit new
  commercial systems based on an Intel development kit reference design.

This reflects the partner-scaled principle: Intel designs the reference;
ecosystem partners commercialize, ruggedize, and scale.

### Consequences

**Positive**

- Developers can identify and order validated kits with known fit and status.
- Partners have a clear, open path to commercialize Intel reference designs.
- Kits align with Hardware Catalog entries (ADR-0005) and blueprints (ADR-0008).

**Negative / Trade-offs**

- Commercial availability depends on partners, not Intel directly.
- Requires maintaining reference-design documentation and a partner contribution workflow.
- Each kit must carry Edge Pack enablement (ADR-0007) and blueprint validation (ADR-0008).

## More Information

- Edge Pack configuration per kit is decided in ADR-0007.
- Kit-to-blueprint compatibility feeds from ADR-0008 (§8.5 Development Kit Catalog feed).
- Detailed kit reference-design specifications are maintained in the catalog itself.
