# Roadmap

## Purpose
Track staged modernization while preserving current reproducibility and contributor usability.

## Current State
This roadmap is directional. It is not a design-spec replacement and does not redefine current runtime behavior.

## How To
### Phase 0: Baseline + Documentation
- [ ] Validate compile/run paths on contributor machines.
- [ ] Keep setup, runbook, and config references current.
- [ ] Capture baseline runtime/perf notes for future comparisons.

### Phase 1: Headless-First Foundation
- [ ] Separate simulation logic from GUI dependencies where practical.
- [ ] Make headless workflows easier for automation and CI.
- [ ] Make headless debugging and validation workflows first-class and easier than GUI-dependent workflows.
- [ ] Add targeted tests around deterministic seeds and turn progression.
- [ ] Implement items in [Headless-First Plan](./headless-first-plan.md).

### Phase 2: Config and Patch Alignment
- [ ] Audit config constants against current target patch expectations.
- [ ] Stage gameplay-impacting changes in small batches.
- [ ] Document each delta with rationale and validation notes.

### Phase 3: Maintainability
- [ ] Improve contributor onboarding and structural consistency.
- [ ] Introduce lightweight CI checks for build/doc integrity.
- [ ] Formalize release/versioning policy for NeoTribes.
- [ ] Keep GUI as an optional showcase/demo layer, not a required validation path.

## References
- [Docs Index](./README.md)
- [Architecture](./architecture.md)
- [Headless-First Plan](./headless-first-plan.md)
- [Configs](./configs.md)
- [Standards](./standards.md)

## Known Gaps
- Timeline and milestone dates are intentionally not fixed yet.
- Ownership per phase is not assigned in this document.
