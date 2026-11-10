# ADR-0010: Consolidate Physical AI model enablement around upstream-first

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; AI Frameworks Engineering; Platform Architecture
- **Related ADRs:** [0004](0004-open-and-upstream-by-default.md), [0002](0002-five-layer-platform-architecture.md), [0008](0008-blueprint-first-benchmarking.md), [0011](0011-evolve-geti-into-edge-vision-ai-stack.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 10 (Requirement 6)

## Context and Problem Statement

Customers need a consistent way to identify Physical AI models supported on Intel
platforms, understand their compatibility and support status, and run OpenVINO
export and inference. Today, some model integrations depend on specific repository
forks or commits, with patches maintained in the Robotics AI Suite repository.
This fragments the enablement experience and blurs the line between officially
supported integrations and experimental examples.

The platform needs a unified model enablement experience that prioritizes upstream
contributions, uses approved release paths, and clearly documents the support
boundaries of patch-based integrations. Here, *consolidation* refers to the
customer-facing enablement and support experience; it does **not** require moving
all model source code into one repository.

## Decision Drivers

- Suite-specific patches diverge from the upstream-first strategy (ADR-0004) and create maintenance burden.
- Patches are not consistently validated against upstream main-branch changes.
- Unclear release/support status undermines a coherent customer offering.
- Integrations outside the approved process lack a path to supported distribution.

## Considered Options

1. **Keep fork/patch-per-model in the Suite repo** — status quo.
2. **Move all model source into one Intel monorepo** — physical code consolidation.
3. **Upstream-first enablement with approved alternative release paths** —
   consolidate the *experience*, prioritize upstream, and bound patch exceptions.

## Decision Outcome

Chosen option: **Upstream-first enablement with approved alternative release paths.**
The Suite provides a unified model enablement experience with these requirements:

- **Prioritize upstream enablement.** Contribute OpenVINO export, inference, and
  optimization changes to the original model repository wherever feasible.
- **Define an approved alternative release path.** Where upstream integration is
  not feasible, use an approved distribution/maintenance path (for example Physical
  AI Studio or Physical AI Framework), subject to the applicable release process.
- **Provide a consistent interface.** Expose supported integrations through a
  common customer-facing interface; for models that cannot receive first-party
  library support, assess the proposed Physical AI Studio interface while clearly
  distinguishing them from first-party-supported models.
- **Document compatibility and support.** For each integration, publish the model
  version/commit, required patches, supported OpenVINO versions and target
  hardware, setup instructions, known limitations, and support status.
- **Maintain patch-based exceptions** only where needed, with a named maintenance
  owner, a pinned upstream version, reproducible export/inference checks, and a
  defined revalidation policy.

### Consequences

**Positive**

- Clear, consistent customer experience with explicit support boundaries.
- Reduced divergence and maintenance burden by favoring upstream.
- A defined path from experimental integration to supported distribution.

**Negative / Trade-offs**

- Upstream acceptance is not guaranteed, so some approved-path exceptions remain.
- Requires governance to track pinned versions, owners, and revalidation.
- Does not eliminate all patches; exceptions must stay discoverable and bounded.

## More Information

- Perception/vision scope is handled separately by the Edge Vision AI Stack (ADR-0011); keep the boundaries distinct.
- Model versions declared supported here must match those referenced by blueprints (ADR-0008).
- The models enabled here are orchestrated into a running robot by the RobotRuntime framework (ADR-0012).
