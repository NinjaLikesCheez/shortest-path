# Agents

## Cursor Cloud specific instructions

This is a **Shortest Path** RuneLite plugin — a single Java Gradle project (not a monorepo). No external services, databases, or Docker containers are needed.

### Key commands

| Action | Command |
|--------|---------|
| Build | `./gradlew build` |
| Test (206 unit tests) | `./gradlew test` |
| Test + coverage report | `./gradlew jacocoTestReport` |
| TSV data lint | `python3 scripts/check_tsv.py` |
| Coordinate JSON dump | `python3 scripts/dump_transport_coordinates.py` |
| Launch RuneLite client (GUI) | `./gradlew runelite` |

### Non-obvious caveats

- Tests require `-Xms1g -Xmx8g` JVM args (already configured in `build.gradle`). The `PathfinderTest` loads full collision maps into memory and is the heaviest test class (~8s).
- `./gradlew runelite` requires a GUI (X11/display). It launches the full RuneLite client with the plugin loaded via `ShortestPathPluginTest` main class. This is for manual/visual testing only.
- The project uses `latest.release` for the RuneLite dependency version, resolved from `repo.runelite.net`. Builds may occasionally break if RuneLite pushes an incompatible API change.
- Python 3 is needed only for the helper scripts in `scripts/` (TSV linting, coordinate dumping). It is not needed for building or testing the Java code.
- Deprecation warnings during compilation (`-Xlint:deprecation`) and unchecked operation warnings are expected and non-blocking.
