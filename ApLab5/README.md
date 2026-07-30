# ApLab5 — Paint (Inheritance vs. Duplication)

Two versions of a console “paint” demo that store circles, rectangles, and triangles and print area/perimeter-style output. **BadPaint** keeps separate lists and duplicated APIs; **GoodPaint** uses an inheritance hierarchy and polymorphism.

Part of the [AUT AP Lab](../README.md) series. Course materials: `Session5.pdf`.

---

## Motivation

Compare a design without shared types (type-specific collections and methods) to one with an abstract `Shape` hierarchy so `Paint` can treat all shapes uniformly.

---

## Projects

| Project | Approach |
|---------|----------|
| [BadPaint](#badpaint) | Separate `ArrayList`s for `Circle`, `Triangle`, `Rectangle`; `addCircle` / `addTriangle` / `addRectangle` |
| [GoodPaint](#goodpaint) | `Shape` ← `Circle`, `Polygon` ← `Rectangle` / `Triangle`; single `addShape(Shape)` |

Both are **console demos** (text output only—no graphical canvas).

---

## BadPaint

### Components

- `Circle`, `Rectangle`, `Triangle` — each has its own `draw`, `calculateArea`, `calculatePerimeter`, `equals` / `toString`
- `Paint` — three lists; `drawAll` / `printAll`
- `Main` — constructs sample shapes and exercises `Paint`

### Build and run

```bash
cd BadPaint/src
javac *.java
java Main
```

---

## GoodPaint

### Class hierarchy

```
Shape (abstract)
├── Circle
└── Polygon (abstract, sides: ArrayList<Double>)
    ├── Rectangle  (+ isSquare())
    └── Triangle   (+ isEquilateral())
```

### Components

| Class | Role |
|-------|------|
| `Shape` | Abstract `toString`, `equals`, area/perimeter; shared `draw()` |
| `Polygon` | Varargs sides; shared side listing / equality |
| `Paint` | `ArrayList<Shape>`; `drawAll`, `printAll`, `describeEqualSides` |
| `Main` | Adds sample shapes; draws, prints, lists squares / equilateral triangles |

`describeEqualSides` prints rectangles that pass `isSquare()` and triangles that pass `isEquilateral()`.

### Build and run

```bash
cd GoodPaint/src
javac *.java
java Main
```

`APLab.txt` in this folder only contains a short note (“master of ApLab projects”), not design docs. A `.uml` file is present as a design artifact.

---

## Technology stack

- Java SE
- Inheritance, abstract classes, `instanceof`, method overriding
- `java.util.ArrayList`, `Objects`, `Math`

---

## Design decisions illustrated

- **BadPaint:** Adding a new shape type requires a new list and new add/draw/print loops in `Paint`.
- **GoodPaint:** New shapes implement `Shape` (and optionally extend `Polygon`); `Paint` stays unchanged for draw/print. Equal-side reporting still uses `instanceof` for rectangle/triangle-specific checks.

---

## Limitations / caveats

- Area and perimeter formulas in several classes do not match standard geometry (e.g. circle area/perimeter appear swapped; polygon “area” may sum sides). Treat outputs as lab exercise results, not correct geometry.
- No graphical rendering—`draw` prints metrics to the console.
- No unit tests.

---

## Related

- [Main README](../README.md)
- Previous: [ApLab4](../ApLab4/) · Next: [ApLab6](../ApLab6/) (CRC cards)
