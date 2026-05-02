# Setup

## Purpose
Define reproducible local environment setup for contributors working on current NeoTribes behavior.

## Current State
- Repository is an upstream-based Java project without Maven/Gradle wrapper.
- Source root is `src/`.
- JSON dependency is vendored as `lib/json.jar`.

## How To
### Local Environment
1. Install Java 8+.
2. Clone repository.
3. Open project in IDE and mark `src/` as source root.
4. Add `lib/json.jar` to classpath.

### Command-Line Build

```bash
mkdir -p out
javac -cp lib/json.jar -d out $(find src -name '*.java')
```

### Baseline Validation Checklist
- [ ] Project compiles with `javac` command above.
- [ ] `Tournament` runs from command line with `tournament.json`.
- [ ] `Play` command is runnable in environments with GUI/display support.
- [ ] Contributor can locate and edit JSON config files in repository root.

### Output and Data Paths
- Level files: `levels/`
- Game saves (if enabled): `save/<game-seed>/<tick>_<activeTribe>/game.json`
- Terrain probabilities: `terrainProbs.json`

## References
- [Quickstart](./quickstart.md)
- [Runbook](./runbook.md)
- [Troubleshooting](./troubleshooting.md)
- [IO JSON loader](../src/utils/file/IO.java)
- [Game save writer](../src/core/game/GameSaver.java)

## Known Gaps
- No one-command bootstrap script currently exists for local development.
- JVM version compatibility matrix is not yet formalized.
