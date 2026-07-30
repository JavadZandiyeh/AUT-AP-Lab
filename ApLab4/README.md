# ApLab4 — Voting System

Interactive console application for creating polls, casting votes, and viewing tallies. Uses Java collections and the bundled Jalali (Persian) calendar library for vote timestamps.

Part of the [AUT AP Lab](../README.md) series.

---

## Problem

Support multiple polls with either single-choice or multi-choice answers, record who voted, and report how many votes each option received.

---

## Key features

| Feature | Status |
|---------|--------|
| Create a poll (question, type, space-separated choices) | Implemented |
| Vote as a named person (single or multi choice by type) | Implemented |
| Print current results (counts per choice) | Implemented |
| Prevent a person from voting twice on the same poll | Partial — uses `ArrayList.contains` on `Person` without custom `equals`/`hashCode` (identity-based) |
| `randomVote` API on `Voting` / `VotingSystem` | Implemented in model; **not** exposed in the console menu |
| Jalali calendar date/day on each `Vote` | Implemented via `ir.huri.jcal.JalaliCalendar` |

---

## Main components

| Class | Role |
|-------|------|
| `Person` | Voter first/last name |
| `Vote` | Person + date string; `equals` based on person |
| `Voting` | One poll: type `0` (single) / `1` (multi), `HashMap<String, HashSet<Vote>>` |
| `VotingSystem` | List of polls; create, vote, print |
| `Main` | Menu: Add voting / Vote / Result / Exit |

### Data model (simplified)

```
VotingSystem
 └── votingList: ArrayList<Voting>
      └── Voting
           ├── question, type
           ├── voters: ArrayList<Person>
           └── listOfVotesToChoices: HashMap<choice, HashSet<Vote>>
```

---

## Technology stack

- Java SE (`ArrayList`, `HashMap`, `HashSet`, `Scanner`, `Random`)
- **JalaliCalendar 1.3.1** (`JalaliCalendar-1.3.1.jar` in `src/`)

---

## Repository layout

```
ApLab4/
├── ApLab-Session4.pdf
└── VotingSystem/
    └── src/
        ├── Main.java
        ├── Person.java
        ├── Vote.java
        ├── Voting.java
        ├── VotingSystem.java
        └── JalaliCalendar-1.3.1.jar
```

---

## Build and run

```bash
cd VotingSystem/src
javac -cp "JalaliCalendar-1.3.1.jar:." *.java
java -cp "JalaliCalendar-1.3.1.jar:." Main
```

On Windows, use `;` instead of `:` in the classpath.

### Menu

1. **Add voting** — question, type (`0` or `1`), then choices as space-separated words  
2. **Vote** — name, poll index, then choice word(s)  
3. **Result** — poll index → prints `choice:count`  
4. **Exit** (labeled `Esit` in the prompt)

Poll indices are 0-based (`votingList.get(i)`).

---

## Limitations

- Input normalization lowercases text and collapses whitespace; multi-word choice labels are awkward because choices are split on spaces.
- `randomVote` indexes the map incorrectly if used (random int used as a map key rather than selecting among key set entries).
- No file persistence; all state is in memory for the process lifetime.
- Session PDF is course material, not runtime documentation.

---

## Related

- [Main README](../README.md)
- Previous: [ApLab3](../ApLab3/) · Next: [ApLab5](../ApLab5/)
