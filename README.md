# NeoTribes

## About
NeoTribes is a fork of the original [Tribes](https://github.com/GAIGResearch/Tribes) framework.

This fork is focused on:
- modernizing the codebase for maintainability and efficiency,
- improving headless execution workflows,
- aligning config/game behavior with recent Polytopia expectations,
- expanding contributor-focused documentation.

As of May 2, 2026, NeoTribes remains intentionally close to upstream Tribes while documentation and baseline workflows are being strengthened.

## Documentation
Primary documentation is in [`docs/`](./docs):
- [Docs Index](./docs/README.md)
- [Quickstart](./docs/quickstart.md)
- [Setup](./docs/setup.md)
- [Runbook](./docs/runbook.md)
- [Configs](./docs/configs.md)
- [Architecture](./docs/architecture.md)
- [Extending Agents](./docs/extending-agents.md)
- [Troubleshooting](./docs/troubleshooting.md)
- [Standards](./docs/standards.md)

## Quick Start
```bash
mkdir -p out
javac -cp lib/json.jar -d out $(find src -name '*.java')
java -cp out:lib/json.jar Tournament
```

## Project Files
- Runtime sources: `src/`
- Level files: `levels/`
- Runtime configs: `play.json`, `tournament.json`, `elites.json`, `terrainProbs.json`
- Changelog: [CHANGELOG.md](./CHANGELOG.md)
- Contributing: [CONTRIBUTING.md](./CONTRIBUTING.md)

## Upstream Note
Legacy upstream usage details previously in this file are now maintained as contributor-oriented docs under [`docs/`](./docs).
