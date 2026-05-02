# Troubleshooting

## Purpose
Provide practical fixes for common setup and runtime errors in current NeoTribes workflows.

## Current State
Most issues are related to Java environment, classpath configuration, GUI/headless mismatch, and JSON configuration validity.

## How To
### `java.awt.HeadlessException` when running `Play`
Symptom:
- `No X11 DISPLAY variable was set` and stack trace from `gui.GUI`.

Cause:
- `Play` uses GUI mode by default and requires a display server.

Fix options:
- Run on a machine/session with display support.
- Use `Tournament` or `RunElites` for headless execution.
- Set `Constants.VISUALS = false`, rebuild, rerun.

### `ClassNotFoundException` for `Play`/`Tournament`
Symptom:
- `Could not find or load main class ...`

Cause:
- Compile output missing or classpath incorrect.

Fix:

```bash
mkdir -p out
javac -cp lib/json.jar -d out $(find src -name '*.java')
java -cp out:lib/json.jar Tournament
```

### JSON Config Parse Errors
Symptom:
- `Malformed JSON config file` or stack traces during startup.

Cause:
- Missing keys, invalid types, or malformed JSON syntax.

Fix:
- Compare edited config against defaults in `play.json`, `tournament.json`, `elites.json`.
- Ensure `Players` and `Tribes` arrays have equal length.
- Ensure numeric fields remain numeric (not quoted strings unless expected by parser).

### Dependency/ClassPath Issues in IDE
Symptom:
- Missing `org.json` classes.

Cause:
- `lib/json.jar` not attached to project/module dependencies.

Fix:
- Add `lib/json.jar` to IDE module classpath.
- Ensure `src/` is a source root.

## References
- [Quickstart](./quickstart.md)
- [Setup](./setup.md)
- [Runbook](./runbook.md)
- [Configs](./configs.md)
- [Constants](../src/core/Constants.java)

## Known Gaps
- Troubleshooting does not yet include performance tuning guidance by agent type.
- Troubleshooting does not yet cover Windows-specific shell/path examples.
