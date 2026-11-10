# ADR-0002: Organize the platform as five software layers on Intel hardware

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Platform Architecture; Robotics & Physical AI Product Management
- **Related ADRs:** [0001](0001-unified-end-to-end-robotics-physical-ai-suite.md), [0003](0003-consolidate-compute-one-robot-one-soc.md), [0004](0004-open-and-upstream-by-default.md), [0008](0008-blueprint-first-benchmarking.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 4

## Context and Problem Statement

The unified Suite (ADR-0001) must present a coherent technical structure that
spans everything from operating systems and drivers to complete robot
blueprints. Without an agreed layering, teams would expose inconsistent
interfaces, version components independently, and make it impossible to state
clearly what was validated against which hardware.

A layered architecture is needed so that each layer exposes stable interfaces to
the layer above, is versioned as part of a platform release, and is validated
against specific hardware entries in the catalogs.

## Decision Drivers

- Need stable, versioned interfaces between concerns (OS, safety/RT, middleware, AI, solutions).
- Validation must bind a software release to specific hardware entries.
- Cross-cutting services (tooling, simulation, benchmarking, lifecycle) must span all layers.
- Customers need a clear mental model that maps to how they build robots.

## Considered Options

1. **Monolithic reference stack** — one bundled, tightly coupled distribution.
2. **Ad-hoc component catalog** — a loose collection of parts without defined layering.
3. **Five-layer architecture** — explicit layers with stable interfaces on top of
   the hardware platforms, with cross-cutting services spanning layers.

## Decision Outcome

Chosen option: **Five-layer architecture.** The platform is organized as five
software layers running on Intel hardware platforms and development kits:

| Layer | Scope |
| ----- | ----- |
| **Layer 5 — Robotics Blueprints** | Complete reference solutions per robot type (humanoids, AMRs, arms, mobile manipulators, warehouse, service) with validated hardware, software, models, and deployment guidance. |
| **Layer 4 — AI** | Vision AI, generative AI, Physical AI (VLA policies, IL/RL), agentic/multi-agent systems, world models, perception and planning frameworks (OpenVINO, Physical AI framework/Studio, PyTorch XPU, model zoo, SLAM/motion-planning libraries). |
| **Layer 3 — Middleware** | Robotics middleware, communication, zero-copy IPC, orchestration and containerization. |
| **Layer 2 — Core Robotics Services** | Functional safety, security, real-time computing, industrial communication, device management, monitoring/diagnostics (Intel TCC, TSN, PREEMPT_RT, hypervisor partitioning, EtherCAT/CAN-FD). |
| **Layer 1 — Foundation** | Operating systems, drivers, BSPs, firmware, device management, delivered through an Intel-managed distribution (enhanced Edge Pack). |
| **Hardware platforms** | Intel SoCs, processors, GPUs, reference designs, developer kits, partner systems (the catalogs in ADR-0005 and ADR-0006). |

Each layer exposes stable interfaces upward, is versioned per platform release,
and is validated against catalog hardware. Tooling, simulation, benchmarking,
and lifecycle management are cross-cutting services spanning all layers.

### Consequences

**Positive**

- Clear separation of concerns and stable, versioned contracts between layers.
- Validation and lifecycle can be reasoned about per layer and per hardware entry.
- Customers can adopt or substitute at a layer boundary.

**Negative / Trade-offs**

- Interface stability imposes governance and change-management overhead.
- Cross-cutting services must be designed to span layers without leaking coupling.
- Detailed requirements for Layers 2–4 are deferred to future PRD versions.

## More Information

- Layer 1 delivery is decided in ADR-0007 (Edge Pack).
- Layer 5 blueprints and their validation are decided in ADR-0008.
- The AI layer's model enablement and vision stack are refined in ADR-0010 and ADR-0011.
