# Configs

## Purpose
Provide a structured reference for runtime configuration files and core rule constants used by the current NeoTribes implementation.

## Current State
Configuration is split between:
- Root JSON files read at runtime.
- Java constants in `Constants.java` and `TribesConfig.java`.

## How To
### Root JSON Config Files

#### `play.json`
| Name | Type | Value/Default | Effect | Source |
| --- | --- | --- | --- | --- |
| `Run Mode` | `string` | `PlayLG` | Selects single-game mode (`PlayLG`, `PlayFile`, `Replay`). | `play.json` |
| `Run Mode comment` | `string` | `PlayLG / PlayFile / Replay` | Human note only. | `play.json` |
| `Runtime Mode` | `string` | `headless` | Selects runtime mode (`headless` or `gui`) for Play execution. Defaults to headless when missing. | `play.json` |
| `Runtime Mode comment` | `string` | `headless / gui` | Human note only. | `play.json` |
| `Progressive Bias` | `boolean` | `true` | Enables pMCTS progressive bias behavior. | `play.json` |
| `Pruning` | `boolean` | `true` | Enables pruning in portfolio MCTS. | `play.json` |
| `K init mult` | `number` | `0.5` | pMCTS init coefficient. | `play.json` |
| `T mult` | `number` | `2.0` | pMCTS exploration coefficient. | `play.json` |
| `A mult` | `number` | `1.5` | pMCTS action coefficient. | `play.json` |
| `B` | `number` | `1.3` | pMCTS bias coefficient. | `play.json` |
| `Game Mode` | `string` | `Capitals` | Selects game mode (`Capitals` or `Score`). | `play.json` |
| `Rollouts` | `boolean` | `false` | Enables MCTS rollouts. | `play.json` |
| `Search Depth` | `number` | `20` | Rollout/individual length for search agents. | `play.json` |
| `Force End` | `boolean` | `false` | Forces turn end after fixed action count in some agents. | `play.json` |
| `Population Size` | `number` | `1` | Population size for population-based agents (RHEA). | `play.json` |
| `Players` | `string[]` | `["OEP","pMCTS"]` | Ordered player controller list. | `play.json` |
| `Tribes` | `string[]` | `["Xin Xi","Imperius"]` | Ordered tribe list, length must match `Players`. | `play.json` |
| `Verbose` | `boolean` | `false` | Controls runtime log verbosity (`Constants.VERBOSE`). | `play.json` |
| `Replay File Name` | `string` | `save/.../game.json` | Savegame path used when `Run Mode=Replay`. | `play.json` |
| `Level File` | `string` | `levels/SampleLevel.csv` | CSV level path used when `Run Mode=PlayFile`. | `play.json` |
| `Game Seed` | `string/number` | `-1` | Seed for game RNG, random if `-1`. | `play.json` |
| `Agents Seed` | `string/number` | `-1` | Seed for agent RNG, random if `-1`. | `play.json` |
| `Level Seed` | `string/number` | `-1` | Seed for level generation, random if `-1`. | `play.json` |

Example `play.json` snippets:

Headless (default contributor mode):

```json
{
  "Run Mode": "PlayLG",
  "Runtime Mode": "headless"
}
```

GUI showcase mode:

```json
{
  "Run Mode": "PlayLG",
  "Runtime Mode": "gui"
}
```

#### `tournament.json`
| Name | Type | Value/Default | Effect | Source |
| --- | --- | --- | --- | --- |
| `Game Mode` | `string` | `Capitals` | Tournament game mode. | `tournament.json` |
| `Repetitions` | `number` | `20` | Games per seed/matchup. | `tournament.json` |
| `Rollouts` | `boolean` | `false` | Enables MCTS rollouts. | `tournament.json` |
| `Search Depth` | `number` | `20` | Agent search horizon parameter. | `tournament.json` |
| `Force End` | `boolean` | `false` | Forces short turns in some agents. | `tournament.json` |
| `Population Size` | `number` | `1` | Population size for RHEA-like agents. | `tournament.json` |
| `Players` | `string[]` | `["MCTS","pMCTS"]` | Ordered player type list. | `tournament.json` |
| `Tribes` | `string[]` | `["Xin Xi","Imperius"]` | Ordered tribe list, length must match players. | `tournament.json` |
| `Shift Tribes` | `boolean` | `true` | Rotates player position assignment between games. | `tournament.json` |
| `Verbose` | `boolean` | `false` | Enables verbose logging. | `tournament.json` |
| `Level Seeds` | `string[]` | list of seed strings | Seed list for level generation across tournament runs. | `tournament.json` |
| `Progressive Bias` | `boolean` | `true` | pMCTS progressive bias toggle. | `tournament.json` |
| `Pruning` | `boolean` | `true` | pMCTS pruning toggle. | `tournament.json` |
| `K init mult` | `number` | `0.5` | pMCTS init coefficient. | `tournament.json` |
| `T mult` | `number` | `2.0` | pMCTS exploration coefficient. | `tournament.json` |
| `A mult` | `number` | `1.5` | pMCTS action coefficient. | `tournament.json` |
| `B` | `number` | `1.3` | pMCTS bias coefficient. | `tournament.json` |

#### `elites.json`
| Name | Type | Value/Default | Effect | Source |
| --- | --- | --- | --- | --- |
| `Elites features` | `string[]` | `["RESEARCH_PROGRESS","OWNED_TILES_PROGRESS"]` | Feature dimensions for MAP-Elites archive. | `elites.json` |
| `nWeights` | `number` | `11` | Number of weights evolved by MAP-Elites runner. | `elites.json` |
| `Elites iterations` | `number` | `20` | Number of MAP-Elites iterations. | `elites.json` |
| `Random inits` | `number` | `1` | Number of random initial samples. | `elites.json` |
| `Repetitions` | `number` | `2` | Games per seed setup inside elites runs. | `elites.json` |
| `Progressive Bias` | `boolean` | `true` | pMCTS progressive bias toggle. | `elites.json` |
| `Pruning` | `boolean` | `true` | pMCTS pruning toggle. | `elites.json` |
| `K init mult` | `number` | `0.5` | pMCTS init coefficient. | `elites.json` |
| `T mult` | `number` | `2.0` | pMCTS exploration coefficient. | `elites.json` |
| `A mult` | `number` | `1.5` | pMCTS action coefficient. | `elites.json` |
| `B` | `number` | `1.3` | pMCTS bias coefficient. | `elites.json` |
| `Game Mode` | `string` | `Capitals` | Game mode in each elites-evaluated game. | `elites.json` |
| `Rollouts` | `boolean` | `false` | MCTS rollout flag. | `elites.json` |
| `Search Depth` | `number` | `20` | Search horizon parameter. | `elites.json` |
| `Force End` | `boolean` | `false` | Force short turns in some agents. | `elites.json` |
| `Population Size` | `number` | `20` | Population size used by RHEA-like settings. | `elites.json` |
| `Players` | `string[]` | `["MCTS","pMCTS"]` | Ordered player type list. | `elites.json` |
| `Tribes` | `string[]` | `["Xin Xi","Imperius"]` | Ordered tribe list. | `elites.json` |
| `Shift Tribes` | `boolean` | `true` | Rotates assignment in repeated games. | `elites.json` |
| `Verbose` | `boolean` | `false` | Verbose logging flag. | `elites.json` |
| `Level Seeds` | `string[]` | `["1590557911279"]` | Seed list used for elite evaluations. | `elites.json` |
| `Master` | `boolean` | `false` | Map-Elites mode flag passed to `MapElites`. | `elites.json` |
| `Map folder` | `string` | `map/` | Output folder for elite map files. | `elites.json` |
| `File based` | `boolean` | `true` | File-based archive persistence mode. | `elites.json` |

#### `terrainProbs.json`
| Name | Type | Value/Default | Effect | Source |
| --- | --- | --- | --- | --- |
| `WATER` | `object` | per-tribe multipliers | Terrain/resource probability controls for water. | `terrainProbs.json` |
| `FOREST` | `object` | per-tribe multipliers | Terrain/resource probability controls for forest. | `terrainProbs.json` |
| `MOUNTAIN` | `object` | per-tribe multipliers | Terrain/resource probability controls for mountain. | `terrainProbs.json` |
| `ORE` | `object` | per-tribe multipliers | Resource spawn weighting for ore. | `terrainProbs.json` |
| `FRUIT` | `object` | per-tribe multipliers | Resource spawn weighting for fruit. | `terrainProbs.json` |
| `CROPS` | `object` | per-tribe multipliers | Resource spawn weighting for crops. | `terrainProbs.json` |
| `ANIMAL` | `object` | per-tribe multipliers | Resource spawn weighting for animals. | `terrainProbs.json` |
| `FISH` | `object` | per-tribe multipliers | Resource spawn weighting for fish. | `terrainProbs.json` |
| `WHALES` | `object` | per-tribe multipliers | Resource spawn weighting for whales. | `terrainProbs.json` |

Nested object schema for each top-level entry:

| Name | Type | Value/Default | Effect | Source |
| --- | --- | --- | --- | --- |
| `BASE` | `number` | varies per key | Baseline probability weight before tribe modifier. | `terrainProbs.json` |
| `XIN_XI` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `IMPERIUS` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `BARDUR` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `OUMAJI` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `KICKOO` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `HOODRICK` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `LUXIDOOR` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `VENGIR` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `ZEBASI` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `AI_MO` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `QUETZALI` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |
| `YADAKK` | `number` | varies | Tribe-specific multiplier. | `terrainProbs.json` |

### Core Java Configuration Constants

#### `src/core/Constants.java`
| Name | Type | Value/Default | Effect | Source |
| --- | --- | --- | --- | --- |
| `LOG_STATS` | `boolean` | `true` | Logging/stat verbosity | `src/core/Constants.java` |
| `VERBOSE` | `boolean` | `true` | Logging/stat verbosity | `src/core/Constants.java` |
| `VISUALS` | `boolean` | `true` | Enable/disable GUI | `src/core/Constants.java` |
| `WRITE_SAVEGAMES` | `boolean` | `false` | Savegame/log persistence | `src/core/Constants.java` |
| `DISABLE_NON_HUMAN_GRID_HIGHLIGHT` | `boolean` | `true` | Runtime/GUI/game setting | `src/core/Constants.java` |
| `FRAME_DELAY` | `int` | `0` | Runtime/GUI/game setting | `src/core/Constants.java` |
| `TURN_TIME_LIMITED` | `boolean` | `false` | Turn/time limits | `src/core/Constants.java` |
| `TURN_TIME_MILLIS` | `long` | `10000000` | Turn/time limits | `src/core/Constants.java` |
| `GUI_INFO_DELAY` | `int` | `0` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_PAN_TO_TRIBE` | `boolean` | `false` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_GAME_VIEW_SIZE` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `CELL_SIZE` | `int` | `runtime-initialized` | Runtime/GUI/game setting | `src/core/Constants.java` |
| `GUI_MIN_PAN` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_COMP_SPACING` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_CITY_TAG_WIDTH` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_DRAW_EFFECTS` | `boolean` | `false` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_SIDE_PANEL_WIDTH` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_INFO_PANEL_HEIGHT` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_ACTION_PANEL_HEIGHT` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_TECH_PANEL_HEIGHT` | `int` | `runtime-initialized` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_ACTION_PANEL_FULL_SIZE` | `int` | `350` | GUI behavior/layout | `src/core/Constants.java` |
| `GUI_TECH_PANEL_FULL_SIZE` | `int` | `300` | GUI behavior/layout | `src/core/Constants.java` |
| `SHADOW_OFFSET` | `int` | `1` | Runtime/GUI/game setting | `src/core/Constants.java` |
| `ROUND_RECT_ARC` | `int` | `5` | Runtime/GUI/game setting | `src/core/Constants.java` |
| `GUI_ZOOM_FACTOR` | `int` | `5` | GUI behavior/layout | `src/core/Constants.java` |
| `MAX_TURNS` | `int` | `30` | Turn/time limits | `src/core/Constants.java` |
| `MAX_TURNS_CAPITALS` | `int` | `50` | Turn/time limits | `src/core/Constants.java` |
| `PLAY_WITH_FULL_OBS` | `boolean` | `true` | Observability model | `src/core/Constants.java` |
| `GUI_FORCE_FULL_OBS` | `boolean` | `true` | GUI behavior/layout | `src/core/Constants.java` |

#### `src/core/TribesConfig.java`
| Name | Type | Value/Default | Effect | Source |
| --- | --- | --- | --- | --- |
| `WARRIOR_ATTACK` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WARRIOR_DEFENCE` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WARRIOR_MOVEMENT` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WARRIOR_MAX_HP` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WARRIOR_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WARRIOR_COST` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WARRIOR_POINTS` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ARCHER_ATTACK` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ARCHER_DEFENCE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ARCHER_MOVEMENT` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ARCHER_MAX_HP` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ARCHER_RANGE` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ARCHER_COST` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ARCHER_POINTS` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CATAPULT_ATTACK` | `int` | `4` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CATAPULT_DEFENCE` | `int` | `0` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CATAPULT_MOVEMENT` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CATAPULT_MAX_HP` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CATAPULT_RANGE` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CATAPULT_COST` | `int` | `8` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CATAPULT_POINTS` | `int` | `40` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SWORDMAN_ATTACK` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SWORDMAN_DEFENCE` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SWORDMAN_MOVEMENT` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SWORDMAN_MAX_HP` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SWORDMAN_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SWORDMAN_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SWORDMAN_POINTS` | `int` | `25` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_ATTACK` | `int` | `0` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_DEFENCE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_MOVEMENT` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_MAX_HP` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_HEAL` | `int` | `4` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINDBENDER_POINTS` | `int` | `25` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFENDER_ATTACK` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFENDER_DEFENCE` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFENDER_MOVEMENT` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFENDER_MAX_HP` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFENDER_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFENDER_COST` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFENDER_POINTS` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `KNIGHT_ATTACK` | `int` | `4` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `KNIGHT_DEFENCE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `KNIGHT_MOVEMENT` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `KNIGHT_MAX_HP` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `KNIGHT_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `KNIGHT_COST` | `int` | `8` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `KNIGHT_POINTS` | `int` | `40` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `RIDER_ATTACK` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `RIDER_DEFENCE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `RIDER_MOVEMENT` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `RIDER_MAX_HP` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `RIDER_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `RIDER_COST` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `RIDER_POINTS` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BOAT_ATTACK` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BOAT_DEFENCE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BOAT_MOVEMENT` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BOAT_RANGE` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BOAT_COST` | `int` | `0` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BOAT_POINTS` | `int` | `0` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SHIP_ATTACK` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SHIP_DEFENCE` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SHIP_MOVEMENT` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SHIP_RANGE` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SHIP_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SHIP_POINTS` | `int` | `0` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BATTLESHIP_ATTACK` | `int` | `4` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BATTLESHIP_DEFENCE` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BATTLESHIP_MOVEMENT` | `int` | `3` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BATTLESHIP_RANGE` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BATTLESHIP_COST` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BATTLESHIP_POINTS` | `int` | `0` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SUPERUNIT_ATTACK` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SUPERUNIT_DEFENCE` | `int` | `4` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SUPERUNIT_MOVEMENT` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SUPERUNIT_MAX_HP` | `int` | `40` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SUPERUNIT_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SUPERUNIT_COST` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SUPERUNIT_POINTS` | `int` | `50` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `NUM_STEPS` | `int` | `15` | Map generation/exploration | `src/core/TribesConfig.java` |
| `ATTACK_MODIFIER` | `double` | `4.5` | Combat resolution rules | `src/core/TribesConfig.java` |
| `DEFENCE_BONUS` | `double` | `1.5` | Combat resolution rules | `src/core/TribesConfig.java` |
| `DEFENCE_IN_WALLS` | `double` | `4.0` | Combat resolution rules | `src/core/TribesConfig.java` |
| `VETERAN_KILLS` | `int` | `3` | Combat resolution rules | `src/core/TribesConfig.java` |
| `VETERAN_PLUS_HP` | `int` | `5` | Combat resolution rules | `src/core/TribesConfig.java` |
| `RECOVER_PLUS_HP` | `int` | `2` | Combat resolution rules | `src/core/TribesConfig.java` |
| `RECOVER_IN_BORDERS_PLUS_HP` | `int` | `2` | Combat resolution rules | `src/core/TribesConfig.java` |
| `FARM_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `FARM_BONUS` | `int` | `2` | Building/resource economy | `src/core/TribesConfig.java` |
| `FARM_RES_CONSTRAINT` | `Types.RESOURCE` | `Types.RESOURCE.CROPS` | Building/resource economy | `src/core/TribesConfig.java` |
| `WIND_MILL_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WIND_MILL_BONUS` | `int` | `1` | Building/resource economy | `src/core/TribesConfig.java` |
| `LUMBER_HUT_COST` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `LUMBER_HUT_BONUS` | `int` | `1` | Gameplay rule constant | `src/core/TribesConfig.java` |
| `SAW_MILL_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `SAW_MILL_BONUS` | `int` | `1` | Building/resource economy | `src/core/TribesConfig.java` |
| `MINE_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `MINE_BONUS` | `int` | `2` | Building/resource economy | `src/core/TribesConfig.java` |
| `MINE_RES_CONSTRAINT` | `Types.RESOURCE` | `Types.RESOURCE.ORE` | Building/resource economy | `src/core/TribesConfig.java` |
| `FORGE_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `FORGE_BONUS` | `int` | `2` | Building/resource economy | `src/core/TribesConfig.java` |
| `PORT_COST` | `int` | `10` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `PORT_BONUS` | `int` | `2` | Building/resource economy | `src/core/TribesConfig.java` |
| `PORT_TRADE_DISTANCE` | `int` | `4` | Building/resource economy | `src/core/TribesConfig.java` |
| `CUSTOMS_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CUSTOMS_BONUS` | `int` | `2` | Building/resource economy | `src/core/TribesConfig.java` |
| `MONUMENT_BONUS` | `int` | `3` | Building/resource economy | `src/core/TribesConfig.java` |
| `MONUMENT_POINTS` | `int` | `400` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `EMPERORS_TOMB_STARS` | `int` | `100` | Gameplay rule constant | `src/core/TribesConfig.java` |
| `GATE_OF_POWER_KILLS` | `int` | `10` | Gameplay rule constant | `src/core/TribesConfig.java` |
| `GRAND_BAZAR_CITIES` | `int` | `5` | Gameplay rule constant | `src/core/TribesConfig.java` |
| `ALTAR_OF_PEACE_TURNS` | `int` | `5` | Gameplay rule constant | `src/core/TribesConfig.java` |
| `PARK_OF_FORTUNE_LEVEL` | `int` | `5` | Gameplay rule constant | `src/core/TribesConfig.java` |
| `TEMPLE_COST` | `int` | `20` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `TEMPLE_FOREST_COST` | `int` | `15` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `TEMPLE_BONUS` | `int` | `1` | Building/resource economy | `src/core/TribesConfig.java` |
| `TEMPLE_TURNS_TO_SCORE` | `int` | `3` | Building/resource economy | `src/core/TribesConfig.java` |
| `TEMPLE_POINTS` | `int[]` | `new int[]{100, 50, 50, 50, 150}` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ANIMAL_COST` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `FISH_COST` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `WHALES_COST` | `int` | `0` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `FRUIT_COST` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `ANIMAL_POP` | `int` | `1` | Building/resource economy | `src/core/TribesConfig.java` |
| `FISH_POP` | `int` | `1` | Building/resource economy | `src/core/TribesConfig.java` |
| `WHALES_STARS` | `int` | `10` | Building/resource economy | `src/core/TribesConfig.java` |
| `FRUIT_POP` | `int` | `1` | Building/resource economy | `src/core/TribesConfig.java` |
| `ROAD_COST` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CITY_LEVEL_UP_WORKSHOP_PROD` | `int` | `1` | City progression/scoring | `src/core/TribesConfig.java` |
| `CITY_LEVEL_UP_RESOURCES` | `int` | `5` | City progression/scoring | `src/core/TribesConfig.java` |
| `CITY_LEVEL_UP_POP_GROWTH` | `int` | `3` | City progression/scoring | `src/core/TribesConfig.java` |
| `CITY_LEVEL_UP_PARK` | `int` | `250` | City progression/scoring | `src/core/TribesConfig.java` |
| `CITY_BORDER_POINTS` | `int` | `20` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CITY_CENTRE_POINTS` | `int` | `100` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `PROD_CAPITAL_BONUS` | `int` | `1` | City progression/scoring | `src/core/TribesConfig.java` |
| `EXPLORER_CLEAR_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `FIRST_CITY_CLEAR_RANGE` | `int` | `2` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `NEW_CITY_CLEAR_RANGE` | `int` | `1` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CITY_EXPANSION_TILES` | `int` | `1` | City progression/scoring | `src/core/TribesConfig.java` |
| `POINTS_PER_POPULATION` | `int` | `5` | City progression/scoring | `src/core/TribesConfig.java` |
| `ALLEGIANCE_MAX` | `int` | `60` | Diplomacy system | `src/core/TribesConfig.java` |
| `ATTACK_REPERCUSSION` | `int` | `-5` | Diplomacy system | `src/core/TribesConfig.java` |
| `CAPTURE_REPERCUSSION` | `int` | `-30` | Diplomacy system | `src/core/TribesConfig.java` |
| `CONVERT_REPERCUSSION` | `int` | `-5` | Diplomacy system | `src/core/TribesConfig.java` |
| `MIN_STARS_SEND` | `int` | `15` | Diplomacy system | `src/core/TribesConfig.java` |
| `TECH_BASE_COST` | `int` | `4` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `TECH_DISCOUNT` | `Types.TECHNOLOGY` | `Types.TECHNOLOGY.PHILOSOPHY` | Research cost/progression | `src/core/TribesConfig.java` |
| `TECH_DISCOUNT_VALUE` | `double` | `0.2` | Research cost/progression | `src/core/TribesConfig.java` |
| `TECH_TIER_POINTS` | `int` | `100` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `INITIAL_STARS` | `int` | `5` | Gameplay rule constant | `src/core/TribesConfig.java` |
| `CLEAR_FOREST_STAR` | `int` | `2` | Action economy | `src/core/TribesConfig.java` |
| `GROW_FOREST_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `BURN_FOREST_COST` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `CLEAR_VIEW_POINTS` | `int` | `5` | Unit stat or scoring value | `src/core/TribesConfig.java` |
| `DEFAULT_MAP_SIZE` | `int[]` | `new int[]{-1, 11, 14, 16, 18, 20, 22, 24}` | Map generation/exploration | `src/core/TribesConfig.java` |

## References
- [Runbook](./runbook.md)
- [Architecture](./architecture.md)
- [Play config reader](../src/Play.java)
- [Tournament config reader](../src/Tournament.java)
- [RunElites config reader](../src/RunElites.java)
- [Global constants](../src/core/Constants.java)
- [Gameplay constants](../src/core/TribesConfig.java)

## Known Gaps
- Some constants are implementation-only and not intended for frequent external tuning.
- Config compatibility notes against newer Polytopia patches are not yet filled in.
