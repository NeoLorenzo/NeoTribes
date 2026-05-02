# Extending Agents

## Purpose
Describe the safe workflow to add or modify AI agents in the current codebase.

## Current State
Agent registration is centralized in `Run.java`. Entrypoint JSON files reference string names that are mapped to `Run.PlayerType` values.

## How To
### 1) Implement a New Agent Class
- Place implementation under `src/players/` (or a new subpackage).
- Extend `players.Agent`.
- Implement `Action act(GameState gs, ElapsedCpuTimer ect)`.
- Implement `Agent copy()`.
- Optionally override `result(GameState gs, double reward)`.

### 2) Register Player Type in `Run.java`
Update all three places:
- Add enum value to `Run.PlayerType`.
- Add incoming JSON mapping in `Run.parsePlayerTypeStr(...)`.
- Add constructor path in `Run.getAgent(...)`.

### 3) Validate Config String Usage
- Ensure `play.json`, `tournament.json`, or custom config uses the exact mapped string.
- Confirm player array length still matches tribe array length.

### 4) Smoke Test
- Compile:

```bash
mkdir -p out
javac -cp lib/json.jar -d out $(find src -name '*.java')
```

- Run with a small tournament config that includes the new player type string.

### Common Pitfalls
- Missing one registration step in `Run.java` causes runtime parse failures.
- Returning invalid/infeasible actions in `act(...)` can stall or break turns.
- Forgetting deterministic seed handling can make reproducibility harder.

## References
- [Agent base class](../src/players/Agent.java)
- [Run registration points](../src/Run.java)
- [Runbook](./runbook.md)
- [Troubleshooting](./troubleshooting.md)

## Known Gaps
- No automated template generator exists for new agent scaffolding.
- No dedicated agent conformance test suite exists yet.
