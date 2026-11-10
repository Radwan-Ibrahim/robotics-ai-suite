# ADR-0004: Open and upstream by default

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Platform Architecture; Robotics & Physical AI Product Management; Open Source Program Office
- **Related ADRs:** [0002](0002-five-layer-platform-architecture.md), [0009](0009-real-time-robotics-control.md), [0010](0010-physical-ai-model-enablement.md), [0011](0011-evolve-geti-into-edge-vision-ai-stack.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 4.2

## Context and Problem Statement

Developer mindshare in robotics is platform-driven and community-driven.
Maintaining Suite-specific forks of middleware, control libraries, and model
integrations creates an ongoing maintenance burden, diverges from community
releases, and risks vendor lock-in that customers actively avoid.

The platform needs an explicit, cross-cutting stance on how it engages with open
source so that every requirement — real-time control (ADR-0009), model
enablement (ADR-0010), and the vision stack (ADR-0011) — applies the same policy.

## Decision Drivers

- Open standards and community ecosystems drive adoption and reduce lock-in concern.
- Suite-specific forks are costly to maintain and drift from upstream.
- Customers value a documented, reproducible, non-proprietary upgrade path.
- Intel benefits strategically when its optimizations land upstream.

## Considered Options

1. **Proprietary/forked stack** — maintain Intel-specific forks and components.
2. **Consume upstream passively** — use upstream but keep local patches without contributing back.
3. **Open and upstream by default** — prioritize upstream technologies and open
   standards, contribute improvements upstream, and treat forks as documented,
   time-boxed exceptions.

## Decision Outcome

Chosen option: **Open and upstream by default.** The platform prioritizes
upstream technologies, open standards, and community ecosystems; contributes
improvements upstream; and avoids vendor lock-in. Where direct upstream
integration is not feasible, patch-based exceptions are permitted only with a
named maintenance owner, a pinned upstream version, reproducible build/test
instructions, and a defined revalidation policy (see ADR-0009, ADR-0010, ADR-0011).

### Consequences

**Positive**

- Reduced long-term maintenance cost and reduced drift from community releases.
- Stronger ecosystem goodwill and developer mindshare.
- Customers get a lock-in-free, reproducible upgrade path.

**Negative / Trade-offs**

- Upstream acceptance timelines are outside Intel's direct control.
- Requires governance to review community adoption and project health per release.
- Patch-based exceptions must be actively tracked to avoid becoming de facto forks.

## More Information

- This principle is operationalized for EtherCAT/CAN-FD in ADR-0009, for Physical
  AI models in ADR-0010, and for the Edge Vision AI Stack in ADR-0011.
- Contribution and coverage policy: review adoption and project health at each
  release; add or retire libraries accordingly; submit optimizations to upstream
  maintainers rather than maintaining Suite-specific forks.
