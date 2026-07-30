# ApLab9 — iNote

Desktop notepad application with a Swing UI: tabbed editors, a sidebar of saved files, and persistence under `./notes/`. Supports multiple file I/O styles; the active path uses **Java object serialization** of a `Note` model.

Part of the [AUT AP Lab](../README.md) series.

---

## Problem

Provide a simple GUI for writing notes, saving them to disk, listing saved notes, and reopening them by double-clicking in the sidebar.

---

## Key features

| Feature | Status |
|---------|--------|
| Frame with File menu: New, Save, Exit | Implemented |
| Tabbed `JTextArea` editors | Implemented |
| Sidebar `JList` of files in `./notes/` | Implemented |
| Save selected tab (non-empty) via serialization | Implemented (`FileUtils.objectOutputStream`) |
| Save all tabs on Exit | Implemented |
| Open note on double-click | Implemented (`objectInputStream`) |
| Buffered / byte-stream save & load helpers | Implemented in `FileUtils` but **commented out** at call sites |
| Title/date metadata on `Note` | Partial — serialization uses fixed title `"objectSaving"` and date `yyyyMMdd` |

---

## Architecture

```
Main
 └── gui.CFrame          # JFrame + menu
      └── gui.CMainPanel # BorderLayout: list (west) + JTabbedPane (center)
           └── utils.FileUtils ↔ model.Note (Serializable)
```

Notes directory: `./notes/` (created on class load of `FileUtils` relative to the **working directory** when you run `java`).

---

## Main components

| Type | Role |
|------|------|
| `Main` | Creates visible `CFrame("iNote")` |
| `gui.CFrame` | Menu actions → new tab / save / save-all + exit |
| `gui.CMainPanel` | Tabs, directory list, mouse double-click open |
| `model.Note` | Serializable title, content, date |
| `utils.FileUtils` | Directory listing; reader/writer variants; serialization |

---

## Technology stack

- Java SE 9+ recommended (`InputStream.readAllBytes` in `fileInputStream`)
- Swing (`JFrame`, `JTabbedPane`, `JList`, `JTextArea`, menus)
- `java.io` streams and object serialization
- `SimpleDateFormat` for note dates

---

## Repository layout

```
ApLab9/
└── iNote/
    └── src/
        ├── Main.java
        ├── gui/
        │   ├── CFrame.java
        │   └── CMainPanel.java
        ├── model/
        │   └── Note.java
        └── utils/
            └── FileUtils.java
```

---

## Build and run

Run from a directory where you are happy creating `./notes/` (typically the `iNote` folder or `src`):

```bash
cd iNote/src
javac Main.java gui/*.java model/*.java utils/*.java
java Main
```

1. Type in the default tab → **File → Save**  
2. Confirm a file appears in the left list and under `./notes/`  
3. Double-click a list entry to open its content in a new tab  
4. **File → Exit** saves all tabs then quits  

To exercise buffered or stream-based I/O instead of serialization, swap the commented call sites in `CMainPanel.saveNote` / `MyMouseAdapter` (and use matching write/read pairs).

---

## Limitations

- Serialized files are named from `Note.getContent_All()` string form—awkward filenames possible.
- `fileOutPutStream` writes the **filename bytes**, not the note content (unused while serialization is active).
- No “dirty tab” warning beyond saving everything on exit.
- Package layout requires compiling from `src` with packages on the classpath as shown above.

---

## Related

- [Main README](../README.md)
- Previous: [ApLab8](../ApLab8/) · Next: [ApLab10](../ApLab10/)
