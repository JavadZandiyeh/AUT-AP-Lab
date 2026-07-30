# ApLab3 — Clock Display & Music Organizer

Two console projects practicing **composition** and **collections**.

Part of the [AUT AP Lab](../README.md) series.

---

## Projects

| Project | Purpose |
|---------|---------|
| [ClockDisplay](#clockdisplay) | 24-hour digital clock with hours, minutes, and seconds |
| [MusicOrganizer](#musicorganizer) | In-memory music lists (all tracks + favorites) |

---

## ClockDisplay

### Overview

Simulates a European-style 24-hour clock (`HH:MM:SS`). Built from reusable `NumberDisplay` units that roll over at a configured limit (24 for hours, 60 for minutes/seconds).

### Components

| Class | Role |
|-------|------|
| `NumberDisplay` | Value in `[0, limit)`; `increment()`, zero-padded `getDisplayValue()` |
| `ClockDisplay` | Composes three displays; `timeTick()` advances seconds and cascades |
| `Run` | Reads start time from the user, prints ticks once per second |

### Features

| Feature | Status |
|---------|--------|
| Hours / minutes / seconds with rollover | Implemented |
| Constructor for `00:00:00` or a given time | Implemented |
| Console ticker (`getDisplay` advances then returns time) | Implemented |
| Screen clear between ticks | Windows-oriented (`cmd /c cls`) |
| `setTime` | Present in source but references undefined `hours` / `minutes` fields — not usable as written |

### Build and run

```bash
cd ClockDisplay/src
javac *.java
java Run
```

When prompted (`write your clock:`), enter time as `HH:MM:SS` (eight characters with colons), e.g. `12:30:00`. The program prints ~200 updates, sleeping one second between them.

**Note:** Console clearing uses Windows `cmd`. On macOS/Linux the clear step may fail or behave differently; the clock still prints.

---

## MusicOrganizer

### Overview

Manages two `ArrayList<MusicPlayer>` collections: all music and “love” (favorites). Supports add, list, remove, search, and simulated play/stop. Playback prints messages; it does **not** decode or play audio files (despite an older javazoom comment in `MusicPlayer`).

### Components

| Class | Role |
|-------|------|
| `MusicPlayer` | Path, singer, year placeholders; `startPlaying` / `stop` print status |
| `MusicCollection` | Add/list/remove/search/play helpers over a given `ArrayList` |
| `Main` | Hard-coded demo adding sample paths and exercising collection methods |

### Features

| Feature | Status |
|---------|--------|
| Separate all / favorites lists | Implemented |
| Add, count, list one / list all, remove, search | Implemented |
| Play / stop console messages | Implemented (simulation only) |
| Real MP3 playback via javazoom | Not implemented |

### Build and run

```bash
cd MusicOrganizer/src
javac *.java
java Main
```

No interactive input; `Main` runs a fixed demonstration and prints to stdout.

---

## Technology stack

- Java SE
- `ArrayList`, `Iterator`
- `java.util.concurrent.TimeUnit` (ClockDisplay)
- `ProcessBuilder` (ClockDisplay console clear)

---

## Design notes

- **ClockDisplay** shows composition: the clock delegates digit storage and rollover to `NumberDisplay`.
- **MusicOrganizer** passes the target list into collection methods, so the same operations apply to both libraries.

---

## Limitations

- ClockDisplay `setTime` is broken in the current sources (`hours` / `minutes` are not fields).
- Music “files” are string paths only; no disk or audio library integration.
- Some collection helpers (e.g. index validation, iterator use in remove/play) are fragile educational code—not production-ready.

---

## Related

- [Main README](../README.md)
- Previous: [ApLab2](../ApLab2/) · Next: [ApLab4](../ApLab4/)
