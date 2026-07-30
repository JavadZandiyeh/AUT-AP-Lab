# ApLab2 — Student & Lab

Console program that models students and a lab section: enroll students up to a capacity, then print each student’s details and the average grade.

Part of the [AUT AP Lab](../README.md) series. Introduces basic class design, encapsulation, and fixed-size arrays.

---

## Problem

Represent a lab session with a limited number of seats and compute the average grade of enrolled students from user input.

---

## Key features

| Feature | Status |
|---------|--------|
| `Student` with name, ID, grade | Implemented |
| `Lab` enrollment with capacity check | Implemented |
| Interactive console input via `Scanner` | Implemented |
| Print all students and average grade | Implemented |

---

## Main components

| Class | Role |
|-------|------|
| `Student` | Holds `firstName`, `lastName`, `id`, `grade`; getters/setters and `print()` |
| `Lab` | Fixed `Student[]`, day string, capacity; `enrollStudent`, `calculateAvg`, `print` |
| `Run` | Entry point: reads day/capacity and student data, builds the lab, prints results |

---

## How it works

1. User enters lab **day** and **capacity**.
2. For each seat, the program reads first name, last name, ID, and grade.
3. Students are stored in a `Lab` via `setStudents` / `enrollStudent`.
4. `print()` lists each student and prints the average (integer division).

---

## Technology stack

- Java SE
- `java.util.Scanner`

---

## Repository layout

```
ApLab2/
└── Student/
    └── src/
        ├── Student.java
        ├── Lab.java
        ├── Run.java
        └── README.md   → points here
```

---

## Build and run

```bash
cd Student/src
javac *.java
java Run
```

Example interaction: enter a day (e.g. `Monday`), a capacity (e.g. `2`), then for each student provide name, ID, and grade. Output lists students and an average.

---

## Limitations

- Average uses `int` arithmetic (`avg /= currentSize`).
- `Lab.setStudents` both assigns the array and calls `enrollStudent`, which can inflate `currentSize` relative to a single enrollment path—worth noting if extending the lab.
- No persistence or validation beyond capacity.

---

## Related

- [Main README](../README.md)
- Next: [ApLab3](../ApLab3/) (composition and collections)
