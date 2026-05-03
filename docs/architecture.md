# Architecture

## Purpose
Describe the current runtime architecture and execution flow so contributors can change behavior safely.

## Current State
NeoTribes currently preserves the upstream Tribes architecture with entrypoints in default package classes (`Play`, `Tournament`, `RunElites`) and core simulation logic in `core.game`.

Project direction is headless-first: debugging, validation, and performance work should center on non-GUI execution paths. GUI is retained mainly for showcase/demo usage.

## How To
### High-Level Modules
- `src/core`: game rules, constants, tech tree, diplomacy, types.
- `src/core/game`: board/state lifecycle, loading, saving, game loop.
- `src/players`: agent interfaces and concrete AI implementations.
- `src/gui`: rendering, window input, views.
- `src/utils`: IO, stats, map-elites helpers, misc utilities.

### Startup Paths
1. `Play.main`
- Reads `play.json`.
- Parses players/tribes and mode.
- Initializes `Game` by generated level, CSV level, or replay file.
- Runs through `Run.runGame(Game, KeyController, ActionController)`.
2. `Tournament.main`
- Reads `tournament.json` or passed config path.
- Builds participant/tribe assignment and seeds.
- Runs repeated headless games through `Run.runGame(Game)`.
3. `RunElites.main`
- Reads elites config from first argument.
- Builds a `Runner` that repeatedly launches headless games.
- Executes MAP-Elites loop.

For contributor workflows, `Tournament` and `RunElites` are the primary operational paths for validation and debugging.

### Game Loop Lifecycle
1. `Game.init(...)` constructs `GameState` and players.
2. `Game.run(...)` repeatedly:
- checks end condition,
- processes a tick via `tick(...)`,
- processes each tribe turn via `processTurn(...)`,
- increments tick,
- logs stats and ranking when finished.
3. If GUI is absent/null, `VISUALS` is forced to false in `Game.run`.

### State and Observation Model
- `Game` owns authoritative `GameState`.
- `Game` keeps per-player observations (`gameStateObservations`).
- Agents receive the relevant observed state during action requests.
- `PLAY_WITH_FULL_OBS` and `GUI_FORCE_FULL_OBS` control observability behavior.

### Agent Interaction Points
- Agents extend abstract `players.Agent`.
- Required methods: `act(GameState, ElapsedCpuTimer)` and `copy()`.
- Optional post-game callback: `result(GameState, reward)`.
- Player registration currently flows through `Run.PlayerType`, `Run.parsePlayerTypeStr(...)`, and `Run.getAgent(...)`.

## References
- [Runbook](./runbook.md)
- [Extending Agents](./extending-agents.md)
- [Game](../src/core/game/Game.java)
- [GameState](../src/core/game/GameState.java)
- [Run](../src/Run.java)
- [Agent](../src/players/Agent.java)

## Known Gaps
- Sequence diagrams are not yet included.
- Architecture docs for GUI internals are still minimal.
