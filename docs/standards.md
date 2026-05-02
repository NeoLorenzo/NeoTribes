# Documentation Standards

## Purpose
Define lightweight governance for maintainable documentation in NeoTribes.

## Current State
Docs are markdown files in-repo, maintained alongside code changes.

## How To
### Required Section Contract
All major docs pages must include:
- `Purpose`
- `Current State`
- `How To`
- `References`
- `Known Gaps`

### Style and Tone
- Prioritize concrete steps over abstract descriptions.
- Prefer short sections and explicit commands/paths.
- Use current behavior language; clearly label assumptions.
- Avoid documenting unimplemented future behavior as if complete.

### Linking Conventions
- Use relative links for markdown pages in `docs/`.
- Link to source files when making code behavior claims.
- Keep root `README.md` as an entrypoint and avoid duplicating full runbooks there.

### Update Rules
- If changing run/config behavior, update corresponding docs in same PR.
- If adding/removing config fields, update [Configs](./configs.md).
- If changing extension flow for agents, update [Extending Agents](./extending-agents.md).

### Changelog Rules for Docs
Record in `CHANGELOG.md` when documentation updates are meaningful for users/contributors, including:
- New docs sections or guides.
- Major corrections to setup/run/config instructions.
- Restructuring documentation navigation.

Minor typo-only edits can be omitted from changelog unless part of a larger release note set.

### Docs Versioning Policy
- Doc-only PRs should add a `CHANGELOG.md` entry when they change contributor behavior, workflows, or expected outcomes.
- Doc-only PRs may skip changelog updates when the change is purely editorial (typos, grammar, formatting) and does not alter meaning.
- If uncertain, prefer adding a short changelog line under `Unreleased`.

## References
- [Docs Index](./README.md)
- [Contributing Guide](../CONTRIBUTING.md)
- [Changelog](../CHANGELOG.md)

## Known Gaps
- No automated link-check or markdown lint job is configured yet.
- Formal ADR process is intentionally deferred.
