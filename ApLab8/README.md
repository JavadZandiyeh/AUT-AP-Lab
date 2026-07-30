# ApLab8 — Calculator (UI + Logic)

Swing calculator that extends the ApLab7 layout with **event handling** and an `Operator` model for binary arithmetic. Basic operations work from button clicks; a menu supports exit and clipboard copy.

Part of the [AUT AP Lab](../README.md) series. Builds on [ApLab7](../ApLab7/).

---

## Key features

| Feature | Status |
|---------|--------|
| Basic / Advance tabs (same general layout as ApLab7) | Implemented |
| Digit entry, decimal point, `AC` clear | Implemented |
| Binary ops: `+`, `-`, `*`, `/`, `%` and `=` | Implemented via `Operator` |
| Tooltips on buttons | Implemented |
| File menu: Exit; Copy (Ctrl+A accelerator in code) | Implemented (copy uses basic tab text buffer) |
| Keyboard typing into the text field (appends chars) | Partial — updates internal string; not a full expression parser |
| Advance ops (`shift`, trig, `exp/log`, etc.) | UI present; **not** handled in `ButtonHandler` |
| Nimbus look-and-feel | Same pattern as ApLab7 |

---

## Architecture

Rough MVC-style split noted in code comments:

| Layer | Classes |
|-------|---------|
| View / control | `CalculatorGUI` (nested `ButtonHandler`, `KeyHandler`) |
| Model | `Operator` + `Operators` enum (`SUM`, `MINUS`, `DIVISION`, `DOT`, `MOD`) |
| Entry | `Main` |

Flow for a binary operation: first operand → operator button → second operand → `=` → `Operator.getResult()` written back to the display string.

Separate `Operator` / handler state is kept for Basic (`index 0`) and Advance (`index 1`) tabs.

---

## Technology stack

- Java SE
- Swing + AWT event APIs (`ActionListener`, `KeyAdapter`)
- `java.awt.datatransfer` for clipboard copy

---

## Repository layout

```
ApLab8/
└── Calculator/
    └── src/
        ├── Main.java
        ├── CalculatorGUI.java
        └── Operator.java
```

---

## Build and run

```bash
cd Calculator/src
javac *.java
java Main
```

Example: enter a number, press `+`, enter another number, press `=` — the text field shows the sum.

---

## Limitations

- Only one pending binary operator at a time; no expression trees or parentheses.
- Advance scientific buttons register listeners but have no branches in `actionPerformed` (except shared digit/`PI`/basic ops).
- Division by zero is not specially handled (`float` arithmetic).
- Copy menu copies `text[0]` (basic buffer), not necessarily the active tab.

---

## Related

- [Main README](../README.md)
- Previous UI-only lab: [ApLab7](../ApLab7/) · Next: [ApLab9](../ApLab9/) (iNote)
