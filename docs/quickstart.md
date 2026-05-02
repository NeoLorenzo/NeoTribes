# Quickstart

## Purpose
Get a contributor from clone to a validated local run path as quickly as possible.

## Current State
- Java source is in `src/`.
- External dependency is `lib/json.jar`.
- Primary entry classes are `Play`, `Tournament`, and `RunElites`.
- GUI play requires an X11 display.

### Supported Environments
- Linux/macOS shell workflows are currently the primary documented path.
- GUI gameplay via `Play` requires a display server (X11-compatible environment).
- Headless environments should prefer `Tournament` and `RunElites`.
- Windows-specific setup/run instructions are not yet fully documented.

## How To
### 1) Prerequisites
- Java 8+ (repo validated in this environment with Java 11).
- Bash-compatible shell.

### 2) Compile
From repository root:

```bash
mkdir -p out
javac -cp lib/json.jar -d out $(find src -name '*.java')
```

### 3) Run Tournament (Validated)
Use the default config:

```bash
java -cp out:lib/json.jar Tournament
```

Or pass a custom config path:

```bash
java -cp out:lib/json.jar Tournament /path/to/tournament.json
```

### 4) Run Single-Game via Play

```bash
java -cp out:lib/json.jar Play
```

Notes:
- `Play` reads `play.json` from repository root.
- In headless terminals without X11, `Play` may fail with `java.awt.HeadlessException`.
- For no-GUI runs, use `Tournament`/`RunElites`, or set `Constants.VISUALS = false` and rebuild.

### 5) Run MAP-Elites Mode

```bash
java -cp out:lib/json.jar RunElites /path/to/elites.json
```

## References
- [Setup](./setup.md)
- [Runbook](./runbook.md)
- [Troubleshooting](./troubleshooting.md)
- [Play entrypoint](../src/Play.java)
- [Tournament entrypoint](../src/Tournament.java)
- [RunElites entrypoint](../src/RunElites.java)

## Known Gaps
- No canonical packaged `jar` build script is included.
- CI build instructions are not yet defined.
