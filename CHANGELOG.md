# Changelog

All notable changes to NeoTribes will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project aims to follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Contributor-first documentation expansion with new guides: `docs/quickstart.md`, `docs/runbook.md`, `docs/troubleshooting.md`, `docs/extending-agents.md`, `docs/glossary.md`, and `docs/standards.md`.
- Root-level `CONTRIBUTING.md` with docs maintenance checklist.

### Changed
- Implemented headless-first MVP runtime behavior in `Play`:
- Added explicit `Runtime Mode` support (`headless`/`gui`), defaulting to `headless` when missing.
- Routed headless execution through `Run.runGame(game)` and GUI execution through explicit GUI mode only.
- Reworked `docs/README.md` into a persona-based index and added a documentation section contract.
- Expanded `docs/setup.md`, `docs/architecture.md`, `docs/configs.md`, and `docs/roadmap.md` to reflect current behavior and contributor workflows.
- Simplified root `README.md` into a concise project/docs entrypoint.
- Added docs-governance/versioning clarification in `docs/standards.md`, environment notes in `docs/quickstart.md`, legacy-script guidance in `docs/runbook.md`, and a docs map in `CONTRIBUTING.md`.
- Updated project scope language to make headless execution the primary engineering/debug/validation path, with GUI positioned mainly as a showcase/demo layer.

### Notes
- `play.json` now includes `Runtime Mode` and `Runtime Mode comment` fields.
