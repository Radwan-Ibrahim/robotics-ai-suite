# ADR-0007: Use Intel Edge Pack as the enablement and delivery path

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; Edge Pack Team; Platform Architecture
- **Related ADRs:** [0002](0002-five-layer-platform-architecture.md), [0005](0005-robotics-centric-hardware-catalog.md), [0006](0006-development-kit-catalog.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 7 (Requirement 3)

## Context and Problem Statement

A recurring customer pain point is software integration burden: the operating
system, drivers, real-time kernel, middleware, OpenVINO, and model versions must
be matched manually. The Foundation layer (ADR-0002, Layer 1) must be delivered
as a coherent, validated distribution rather than assembled by the customer.

Intel already ships Edge Pack for operating-system enablement, drivers, firmware,
and platform optimizations. The platform needs to decide how Foundation-layer
enablement is delivered and kept in sync with supported platforms and kits.

## Decision Drivers

- Customers should not hand-assemble OS, drivers, RT kernel, and firmware.
- Every supported platform and kit needs a validated, "platform-ready" configuration.
- Onboarding should verify compatibility automatically.
- Configurations must be revalidated when any dependency changes.

## Considered Options

1. **Document manual setup** — publish instructions and let customers assemble.
2. **Create a new robotics-specific distribution** — build a bespoke delivery mechanism.
3. **Adopt Intel Edge Pack as the recommended delivery path** — define and
   maintain robotics configurations on top of the existing Edge Pack.

## Decision Outcome

Chosen option: **Adopt Intel Edge Pack as the recommended delivery path** for the
operating-system enablement, Intel drivers, firmware, and platform optimizations
required by supported robotics platforms and development kits. The Suite will:

- Define the Edge Pack configuration required for each supported Intel robotics
  platform, reference design, and development kit.
- Work with the Edge Pack team to deliver and maintain these configurations.
- Validate each configuration on its target platform/kit before it is listed as **platform-ready**.
- Publish supported Edge Pack and OS versions, validation status, limitations, and
  setup instructions in the Hardware and Development Kit catalogs.
- Integrate Edge Pack installation and compatibility checks into the onboarding flow.
- Revalidate affected configurations when the platform, kit, OS, Edge Pack release,
  or required driver set changes.

### Consequences

**Positive**

- Eliminates manual OS/driver/firmware matching; faster, reliable onboarding.
- "Platform-ready" status gives customers a trustworthy signal.
- Reuses an existing, maintained Intel delivery mechanism instead of a new one.

**Negative / Trade-offs**

- Creates a dependency on the Edge Pack team's roadmap and release cadence.
- Requires a revalidation pipeline triggered by changes to any dependency.
- Configuration coverage must track every supported platform and kit.

## More Information

- Enablement status is surfaced in the catalogs defined by ADR-0005 and ADR-0006.
- Supports the prototype-to-production continuity goal: the same Foundation image
  carries from development kit to derived production system.
