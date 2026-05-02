# Contributing to NeoTribes

## Purpose
Define a practical contribution workflow for code and documentation updates.

## Current State
NeoTribes is currently close to upstream Tribes. Most active contribution work is documentation hardening, baseline validation, and incremental maintainability improvements.

## Docs Map
Start documentation contributions from:
- [Docs Index](./docs/README.md)
- [Documentation Standards](./docs/standards.md)
- [Configs Reference](./docs/configs.md)
- [Runbook](./docs/runbook.md)

## How To
### Contribution Workflow
1. Create a focused branch.
2. Make changes with clear scope.
3. Run local compile/check commands relevant to your changes.
4. Update docs in the same change set when behavior/config changes.
5. Update `CHANGELOG.md` when change visibility is meaningful to users/contributors.

### Minimum Validation
For most Java/runtime changes:

```bash
mkdir -p out
javac -cp lib/json.jar -d out $(find src -name '*.java')
```

For run-path-impacting changes, also run at least one runtime smoke test (for example `Tournament`).

### Documentation Maintenance Checklist
- [ ] Updated relevant page in `docs/` when runtime behavior changed.
- [ ] Updated [docs/configs.md](./docs/configs.md) when config keys/constants changed.
- [ ] Updated [docs/runbook.md](./docs/runbook.md) when entrypoint behavior changed.
- [ ] Updated [docs/extending-agents.md](./docs/extending-agents.md) when agent registration flow changed.
- [ ] Kept major docs pages compliant with the section contract in [docs/standards.md](./docs/standards.md).

### Changelog Expectations
Update `CHANGELOG.md` for:
- new/removed contributor-facing functionality,
- significant docs additions/corrections,
- config or behavior changes that affect execution or reproducibility.

Small typo-only changes can usually skip changelog updates.

## References
- [Docs Index](./docs/README.md)
- [Documentation Standards](./docs/standards.md)
- [Changelog](./CHANGELOG.md)

## Known Gaps
- CI policy and release workflow are not yet formalized.
- Code style/lint tooling policy is still evolving.
