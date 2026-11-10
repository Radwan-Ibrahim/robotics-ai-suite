# ADR-0009: Enable real-time control through upstream EtherCAT/CAN-FD work

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; Platform Architecture; Real-Time/Industrial Communication Engineering
- **Related ADRs:** [0002](0002-five-layer-platform-architecture.md), [0003](0003-consolidate-compute-one-robot-one-soc.md), [0004](0004-open-and-upstream-by-default.md), [0008](0008-blueprint-first-benchmarking.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 9 (Requirement 5)

## Context and Problem Statement

Industrial robotics requires deterministic control: microsecond-level jitter,
functional safety, and industrial communication (EtherCAT, TSN, CAN-FD) are
non-negotiable. To position Intel platforms as a leading open platform for
deterministic robotics control, the Suite must improve the real-time
communication software customers actually use and prove the result with
validated, reproducible control examples.

Consistent with ADR-0004 (open and upstream by default), this work should land in
widely adopted open-source libraries rather than Suite-specific forks.

## Decision Drivers

- Deterministic cyclic I/O, distributed-clock sync, and bounded jitter are mandatory for industrial control.
- Customers adopt established open-source EtherCAT/CAN-FD stacks; forks would fragment.
- Claims must be provable with measured, reproducible proof-of-capability data.
- Validation should span many actuator types and interfaces.

## Considered Options

1. **Proprietary Intel control stack** — build and maintain Intel-specific masters.
2. **Documentation and tuning guides only** — no code contributions.
3. **Upstream optimization + validated reference applications** — optimize priority
   open-source libraries upstream, publish reference control apps, and publish
   proof-of-capability results.

## Decision Outcome

Chosen option: **Upstream optimization + validated reference applications.**

**Priority EtherCAT libraries:** focus upstream optimization on **SOEM**, **IgH
EtherLab EtherCAT Master**, and **EtherCrab** (MIT/Apache-2.0). Keep KickCAT,
libethercat, and PySOEM as secondary coverage. Prioritize deterministic cyclic
I/O, distributed-clock synchronization, memory efficiency, diagnostics, and Intel
Ethernet integration.

**Priority CAN-FD libraries:** focus upstream optimization on **Linux SocketCAN
with can-utils** and **python-can**. Keep libsocketcan, CANopenNode/CANopenLinux,
Lely CANopen, libcanard/Cyphal, and cantools as secondary coverage. Prioritize
high-rate CAN-FD traffic, timestamping, deterministic send/receive paths,
batching, diagnostics, and multi-bus operation.

**Coverage and contribution policy:** review community adoption and project health
at each release, add or retire libraries accordingly, benchmark the same control
scenarios across supported stacks, and submit optimizations upstream rather than
maintaining Suite-specific forks.

**High-performance reference applications:** publish validated samples for a
single-axis actuator, an OpenArm multi-axis arm, and a high-DoF humanoid
demonstrating the lowest sustainable command-and-feedback cycle time per
configuration. For capable EtherCAT systems, target a **250 µs (4 kHz) cycle with
zero missed deadlines and bounded jitter** under representative concurrent load.
Each sample must show synchronized motion, deadline handling, and fault recovery.

**Actuator test matrix (subject to availability/validation):** DAMIAO (OpenArm);
ROBOTIS DYNAMIXEL; MyActuator RMD/RH; CubeMars AK-series; RobStride; Unitree joint
motors; Feetech smart servos; mjbots moteus; ODrive Pro/S1; VESC- and
SimpleFOC-based open controllers; and industrial EtherCAT servo drives (Beckhoff,
Elmo, Maxon, Kollmorgen, Synapticon, Technosoft).

**Maximum-performance tutorials:** explain how to tune OS, CPU affinity,
scheduling, communication stack, actuator interface, and control application to
reach and verify the lowest stable cycle time; include wiring/setup, position and
torque control, multi-axis synchronization, safety limits, diagnostics, and
troubleshooting for missed deadlines or jitter.

**Proof of real-time capability:** publish the minimum sustained cycle time per
validated platform, library, bus, actuator count, and workload, together with
deadline success rate, worst-case and percentile jitter, CPU utilization, and
results under representative concurrent workloads.

### Consequences

**Positive**

- Differentiates Intel as an open, deterministic control platform with proof, not claims.
- Improvements benefit the broader community and reduce fork maintenance (ADR-0004).
- Broad actuator coverage lowers customer adoption risk.

**Negative / Trade-offs**

- Depends on upstream maintainer acceptance and cadence.
- Maintaining a large actuator test matrix is resource-intensive.
- Hitting 250 µs targets requires careful OS/stack tuning that customers must replicate.

## More Information

- Real-time proof results feed the determinism attributes and T1 tier in ADR-0005, and the control portions of blueprints in ADR-0008.
- Supports single-SoC consolidation (ADR-0003) by proving concurrent control under load.
