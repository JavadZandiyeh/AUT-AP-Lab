# ApLab7 — Calculator (Swing UI)

Graphical calculator shell built with Java Swing. Provides **Basic** and **Advance** tabs, numeric and operator buttons, and a Nimbus look-and-feel when available.

Part of the [AUT AP Lab](../README.md) series.

**Important:** This lab implements the **user interface only**. Buttons and text fields are not wired to listeners or arithmetic logic. Functional calculation appears in [ApLab8](../ApLab8/).

---

## Key features

| Feature | Status |
|---------|--------|
| `JFrame` + `JTabbedPane` (Basic / Advance) | Implemented |
| Display `JTextField`, digit pad, basic operators (`+ − * / % AC`) | Implemented (UI) |
| Advance panel extras (`shift`, `sin/cos`, `tan/cot`, `exp/log`, `PI`, `E`) | Implemented (UI) |
| Nimbus look-and-feel selection | Implemented (fallback prints exception) |
| Button actions / keyboard calculation | Not implemented |

---

## Main components

| Class | Role |
|-------|------|
| `Main` | Sets Nimbus L&F if installed; constructs `CalculatorGUI` |
| `CalculatorGUI` | Builds frame, tabs, absolute-positioned panels and buttons |

Layout uses absolute positioning (`setLayout(null)` + `setBounds`).

---

## Technology stack

- Java SE
- Swing (`JFrame`, `JPanel`, `JTabbedPane`, `JButton`, `JTextField`, `UIManager`)
- AWT `GridLayout`, `Font`

---

## Repository layout

```
ApLab7/
└── Calculator/
    └── src/
        ├── Main.java
        └── CalculatorGUI.java
```

---

## Build and run

Requires a graphical desktop:

```bash
cd Calculator/src
javac *.java
java Main
```

Close the window to exit (`EXIT_ON_CLOSE`).

---

## Limitations

- No `ActionListener`s — clicking buttons does not change the display or compute results.
- Advance keyboard is added only on the Advance tab; Basic tab is a subset of the same layout approach.
- Absolute layout does not resize with the window.

---

## Related

- [Main README](../README.md)
- Next (functional calculator): [ApLab8](../ApLab8/)
