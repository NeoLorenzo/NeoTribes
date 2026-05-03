# Headless-First Implementation Plan

## Purpose
Define the concrete codebase changes required to make NeoTribes headless-first, without covering optimization or debug/validation improvements yet.

## Current State
- `Play` is GUI-oriented by default.
- `Tournament` and `RunElites` already execute headlessly.
- Core simulation and GUI are still coupled through shared entry/runtime paths.

## How To
### MVP (Necessary Now)
#### 1) Lock Runtime Behavior Targets
- [x] Define the exact default command path contributors should run (headless).
- [x] Define the exact explicit GUI command path (showcase/demo only).
- [x] Confirm no default docs command requires display/X11.

#### 2) Add Explicit Runtime Mode Selection
- [x] Add a runtime mode switch for single-game execution (`headless` vs `gui`) in the `Play` configuration path.
- [x] Keep backward compatibility for existing configs by defaulting to headless when mode is absent.
- [x] Ensure mode parsing failure returns a clear startup error message with accepted mode values.

#### 3) Update `Play` Entry Flow to be Headless-First
- [x] Refactor `Play.main` flow so runtime mode is resolved before run invocation.
- [x] Route headless mode to `Run.runGame(game)` (no GUI object creation).
- [x] Route gui mode to existing GUI path (`Run.runGame(game, keyController, actionController)`).
- [x] Keep existing `Run Mode` options (`PlayLG`, `PlayFile`, `Replay`) intact.

#### 4) Prevent Accidental GUI Coupling in Default Path
- [x] Ensure headless mode path never instantiates `KeyController`, `ActionController`, `WindowInput`, or `GUI`.
- [x] Ensure headless mode path can run in environments with no display.
- [x] Ensure GUI mode remains functional for manual showcase/demo use.

#### 5) Make Contributor Commands Headless by Default
- [x] Update root `README.md` quick-start command examples to use headless run path.
- [x] Update `docs/quickstart.md` so first run path is headless and GUI is optional.
- [x] Update `docs/runbook.md` to document explicit GUI launch and default headless flow.

#### 6) Add Minimal Migration Guidance
- [x] Document the new runtime mode key/value in `docs/configs.md`.
- [x] Include one example `play.json` snippet for headless mode.
- [x] Include one example `play.json` snippet for gui showcase mode.

#### 7) Verify MVP Behavior End-to-End
- [x] Build compiles with no new dependencies.
- [x] Default documented command runs successfully in headless environment.
- [x] GUI mode launches only when explicitly requested.
- [x] Existing tournament and elites workflows remain unchanged.

### Deferred (Only If Needed Later)
- [ ] Unify all config parsing across entrypoints into one shared loader.
- [ ] Remove all entrypoint duplication and fully centralize bootstrap logic.
- [ ] Rename/restructure GUI code paths beyond what is required for explicit optional launch.
- [ ] Introduce additional runtime-mode abstractions that are not required for MVP behavior.

### MVP Acceptance Checklist
- [x] A contributor following default docs runs headless by default.
- [x] GUI is not required for normal development flow.
- [x] GUI can still be launched intentionally for showcase/demo usage.
- [x] No required workflow depends on display/X11 availability.
- [x] `Play` supports explicit `headless` and `gui` runtime mode selection.

## References
- [Architecture](./architecture.md)
- [Runbook](./runbook.md)
- [Roadmap](./roadmap.md)
- [Play entrypoint](../src/Play.java)
- [Tournament entrypoint](../src/Tournament.java)
- [Shared runtime](../src/Run.java)

## Known Gaps
- This plan intentionally excludes performance optimization tasks.
- This plan intentionally excludes debug/validation ergonomics tasks.
