# Runbook

## Purpose
Document how runtime entrypoints execute, which config files they read, and what outputs to expect.

## Current State
The main entrypoints are:
- `Play` for single-game sessions (GUI by default).
- `Tournament` for repeated headless evaluations.
- `RunElites` for MAP-Elites workflows.

## How To
### `Play` Flow (Single Game)
1. Reads `play.json`.
2. Parses `Run Mode`: `PlayLG` (generated level), `PlayFile` (CSV level), or `Replay` (saved game JSON).
3. Parses players/tribes arrays and run parameters.
4. Builds `Game` via `Game.init(...)`.
5. Calls `Run.runGame(game, keyController, actionController)`.

Run command:

```bash
java -cp out:lib/json.jar Play
```

Expected output:
- Seed logging (`Game seed`, `Agents random seed`, `Level seed`).
- GUI session if display is available.

### `Tournament` Flow (Headless)
1. Reads `tournament.json` (or first CLI arg if provided).
2. Parses players, tribes, seeds, and search parameters.
3. Iterates through level seeds and repetitions.
4. Runs games with `Run.runGame(game)` (no GUI).
5. Prints per-game and aggregate results.

Run command:

```bash
java -cp out:lib/json.jar Tournament
```

Custom config command:

```bash
java -cp out:lib/json.jar Tournament /path/to/tournament.json
```

Expected output:
- `**** Playing level with seed ...` lines.
- Per-game results and final aggregated stats table.

### `RunElites` Flow (MAP-Elites)
1. Reads config from first CLI arg.
2. Parses elites feature dimensions and search parameters.
3. Executes repeated headless games using weighted portfolio heuristic.
4. Writes/updates elite map artifacts in configured `Map folder`.

Run command:

```bash
java -cp out:lib/json.jar RunElites /path/to/elites.json
```

### Runtime Flags That Affect Behavior
- `Constants.VISUALS`: GUI creation for `Play` flow.
- `Constants.WRITE_SAVEGAMES`: writes save states under `save/`.
- `Constants.VERBOSE`: extra logging in multiple flows.

### Known Legacy Scripts
- `run.sh` and `tribes.sh` are legacy cluster/HPC-oriented scripts from upstream workflows.
- They are not required for local contributor setup and are environment-specific.
- Prefer documented Java entrypoint commands in this runbook for local execution.

## References
- [Quickstart](./quickstart.md)
- [Configs](./configs.md)
- [Play](../src/Play.java)
- [Tournament](../src/Tournament.java)
- [Run](../src/Run.java)
- [RunElites](../src/RunElites.java)
- [Game](../src/core/game/Game.java)

## Known Gaps
- No single canonical CLI wrapper script for local runs.
- Some legacy cluster scripts (`run.sh`, `tribes.sh`) are environment-specific.
