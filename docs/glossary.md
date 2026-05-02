# Glossary

## Purpose
Provide consistent terminology for contributors working on NeoTribes.

## Current State
Terms in this glossary reflect current naming and behavior in the inherited codebase.

## How To
Use this page as a shared vocabulary during code review, issue writing, and doc updates.

### Terms
| Term | Meaning |
| --- | --- |
| `Agent` | An AI or human controller class extending `players.Agent`. |
| `PlayerType` | Enum in `Run.java` used to instantiate agent implementations. |
| `Tribe` | A faction in the game (for example `XIN_XI`, `IMPERIUS`). |
| `GameState` | Core mutable state container for board, tribes, turn/tick progression. |
| `Tick` | Full cycle where each active tribe gets a turn, then game tick increments. |
| `Turn` | One tribe's action sequence until end-turn condition. |
| `Run Mode` | `play.json` setting controlling `Play` execution path (`PlayLG`, `PlayFile`, `Replay`). |
| `PlayLG` | Run mode that generates a level from `Level Seed`. |
| `PlayFile` | Run mode that loads a CSV level file. |
| `Replay` | Run mode that loads a saved game JSON. |
| `Capitals` | Game mode variant focused on capital victory conditions. |
| `Score` | Game mode variant focused on score after turn limit/end state. |
| `pMCTS` | Portfolio MCTS agent mode with optional pruning/progressive bias settings. |
| `Rollouts` | Search behavior toggle used by MCTS variants in configs. |
| `Force End` | Option causing turn cutoff behavior in specific agents. |
| `Level Seed` | Seed used for procedural level generation. |
| `Game Seed` | Seed used for game RNG after map creation. |
| `Agents Seed` | Seed used for agent-level randomness. |
| `Shift Tribes` | Tournament option rotating player-to-position assignments between games. |
| `MAP-Elites` | Illumination/evolution workflow driven through `RunElites`. |

## References
- [Runbook](./runbook.md)
- [Architecture](./architecture.md)
- [Configs](./configs.md)
- [Types definitions](../src/core/Types.java)

## Known Gaps
- No visual glossary/diagram set is included yet.
- Some advanced AI-specific terms are not expanded yet.
