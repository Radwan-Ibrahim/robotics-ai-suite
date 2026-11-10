# ADR-0011: Evolve the Geti AI Libraries to Cover the Full Edge Vision Task Range

- **Status:** Proposed
- **Date:** 2026-10-27
- **Deciders:** Robotics & Physical AI Product Management; Edge Vision / Geti Engineering; Platform Architecture
- **Related ADRs:** [0004](0004-open-and-upstream-by-default.md), [0002](0002-five-layer-platform-architecture.md), [0008](0008-blueprint-first-benchmarking.md), [0010](0010-physical-ai-model-enablement.md)
- **Source:** Robotics AI Suite PRD v0.1, Section 11 (Requirement 7)

## Context and Problem Statement

The Suite needs edge perception models that span the full range of vision tasks
required for robotics — not only the classification, detection, and segmentation
tasks Geti supports today, but also 6D pose estimation, keypoint detection, and
AI-based navigation such as vSLAM. These capabilities are currently scattered,
lack a common training/optimization/inference framework, and have inconsistent
compatibility information and support boundaries.

Geti is built on a set of underlying **AI libraries** (training, optimization,
and inference) that sit beneath the Geti application. The decision is where to
invest. We choose to **evolve the Geti AI libraries** to cover the remaining
vision tasks, rather than changing the Geti application/platform itself. These
new tasks — 6D pose estimation, keypoint detection, and vSLAM-based navigation —
typically run on pretrained or geometry-based models and do not require the
application's interactive features such as dataset collection and fine-tuning, so
the investment belongs in the libraries. This keeps the application stable while
broadening the task range the libraries can train, optimize, and serve. This is a
target product direction, not a claim of existing support.

## Decision Drivers

- Robotics needs the full vision task range (6D pose, keypoints, vSLAM-based navigation), not just Geti's current classification/detection/segmentation tasks.
- The new vision tasks do not require the Geti application features (dataset collection, fine-tuning), so the investment belongs in the AI libraries.
- Investment should target the AI libraries beneath Geti, keeping the Geti application/platform stable.
- Customers need consistent interfaces, compatibility info, reproducible examples, and explicit support boundaries.
- Perception spans multiple modalities and multimodal fusion, not just cameras.
- Upstream-first (ADR-0004) must apply; avoid long-lived forks.
- Perception scope must stay distinct from Physical AI model enablement (ADR-0010).

## Considered Options

1. **Keep the Geti AI libraries as-is** — limited to current classification,
   detection, and segmentation tasks; no coverage of 6D pose, keypoints, or vSLAM.
2. **Extend the Geti application/platform** — add new task UIs and workflows to
   the application itself, coupling new vision tasks to application changes.
3. **Evolve the Geti AI libraries** — broaden the underlying training,
   optimization, and inference libraries to cover the remaining vision tasks
   (6D pose estimation, keypoint detection, vSLAM-based navigation) and additional
   modalities, with explicit support boundaries, while leaving the Geti
   application stable.

## Decision Outcome

Chosen option: **Evolve the Geti AI libraries.** Broaden the underlying training,
optimization, and inference libraries to cover the remaining vision tasks —
6D pose estimation (e.g., FoundationPose), keypoint detection, and AI-based
navigation such as vSLAM — while leaving the Geti application/platform stable.
The libraries provide an extensible architecture for additional modalities and
multimodal perception. Requirements:

- **Scope the change to the AI libraries.** Add the new vision tasks to Geti's
  training/optimization/inference libraries; do not couple them to Geti
  application/platform changes; keep library interfaces usable independently of
  the application. The new tasks do not depend on application features such as
  dataset collection and fine-tuning, so no application changes are required.
- **Establish a unified library structure and repository.** Modular integration
  interfaces and shared packaging/documentation/release practices; maintain
  supported integration assets in the libraries' primary repository wherever
  feasible; a single entry per integration (source repository, version, setup,
  release status, maintenance owner); reference external source/weights rather
  than duplicating them.
- **Define phased task and modality coverage.** Initial plan includes 6D pose
  estimation (FoundationPose), keypoint detection, and vSLAM-based navigation;
  define extension points for depth/3D point clouds, thermal, audio, and inertial
  data, including multimodal fusion where a use case requires it; validate
  feasibility before declaring support.
- **Enable modular multimodal pipelines.** Versioned interfaces for modality-specific
  inputs/outputs, timestamps, coordinate frames, calibration metadata, and
  pre/post-processing; sensor and model adapters added without changing core
  interfaces; document synchronization and missing-input behavior; distinguish
  standalone modality support from validated multimodal combinations.
- **Prioritize upstream contributions.** Contribute reusable export/inference/
  optimization changes to original repositories; keep assets aligned with approved
  upstream versions; avoid unnecessary long-lived forks.
- **Maintain patch-based exceptions.** Where direct integration or upstream
  acceptance is not feasible, provide a versioned patch set with rationale, pinned
  upstream commit, maintenance owner, reproducible build/test instructions, and a
  revalidation policy; keep each exception discoverable and distinct from directly
  maintained support.
- **Publish compatibility and support boundaries.** Record supported and validated
  modality combinations, OSes, runtime/OpenVINO versions where applicable, target
  devices, model precision, sensor/calibration requirements, licenses, known
  limitations, and support status; identify components that run outside OpenVINO.
- **Provide reproducible examples and validation.** Ready-to-run examples and
  versioned test configs; task-appropriate quality/performance criteria for
  6D pose estimation, keypoint detection, vSLAM-based navigation, and each
  modality/fusion pipeline, including end-to-end latency and resource use;
  revalidate on upstream/model/runtime/sensor/hardware changes. vSLAM remains an
  end-to-end pipeline with learned and non-learned components documented separately.
- **Integrate with robotics blueprints.** Reference the same model/pipeline
  versions, modality configurations, and validation evidence used by blueprints
  (ADR-0008); avoid conflicting compatibility claims across the libraries, the
  Suite, and the catalogs; keep perception scope distinct from Physical AI model
  enablement (ADR-0010).

### Consequences

**Positive**

- The Geti AI libraries cover the full robotics vision task range with consistent interfaces and clear support status.
- New tasks, modalities, and adapters can be added without changing core library interfaces or the Geti application.
- Compatibility claims stay consistent with blueprints and catalogs.

**Negative / Trade-offs**

- Evolving the AI libraries to cover new tasks is more work than reusing existing Geti tasks.
- Multimodal fusion adds synchronization, calibration, and validation complexity.
- Must guard against implying full OpenVINO compatibility when only one component is OpenVINO-based.

## Proposed Acceptance Criteria

- 6D pose estimation (FoundationPose), keypoint detection, and vSLAM-based
  navigation each have a library entry identifying an approved direct integration
  or a documented patch-based exception, with an owner and explicit support status,
  and are usable without changes to the Geti application.
- The release plan identifies supported, planned, and out-of-scope tasks,
  modalities, and fusion combinations; at least one additional modality beyond the
  initial camera-based workloads is demonstrated through the documented adapter
  interfaces without changes to core library interfaces.
- Each supported integration passes its published functional, quality, and
  performance criteria on every declared configuration using reproducible instructions.
- Every patch-based exception applies cleanly to its pinned upstream version and
  passes its validation checks; incompatible updates are not promoted as supported.
- Blueprint references resolve to the same versioned integration assets and
  compatibility records published through the libraries, with supported modalities,
  validated combinations, and known limitations clearly stated.

## More Information

- Companion to ADR-0010: this ADR owns perception/vision (the Geti AI libraries); ADR-0010 owns Physical AI policy models.
