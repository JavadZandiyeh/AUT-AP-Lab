# AUT Advanced Programming Lab

Java coursework from the Advanced Programming (AP) lab at Amirkabir University of Technology (AUT). Each `ApLab*` folder is a session exercise covering a specific language or design topic—from basic OOP through Swing GUIs, file I/O, and TCP networking.

**Author:** Mohammad Javad Zandiyeh  
**Language:** Java (standard library + Swing/AWT; one third-party JAR in ApLab4)  
**Build system:** None — compile and run with `javac` / `java`

---

## What this repository is

A collection of standalone lab projects that demonstrate progressive Java skills:

| Lab | Project(s) | Focus |
|-----|------------|-------|
| [ApLab2](ApLab2/) | Student | Classes, encapsulation, arrays, console I/O |
| [ApLab3](ApLab3/) | ClockDisplay, MusicOrganizer | Composition, `ArrayList`, iterators |
| [ApLab4](ApLab4/) | VotingSystem | Collections (`HashMap`, `HashSet`), menu-driven console app, Jalali calendar |
| [ApLab5](ApLab5/) | BadPaint, GoodPaint | Inheritance vs. polymorphism; abstract classes |
| [ApLab6](ApLab6/) | CRC card PDFs | Object-oriented design (no Java code) |
| [ApLab7](ApLab7/) | Calculator | Swing UI layout (Basic / Advance tabs) |
| [ApLab8](ApLab8/) | Calculator | Swing + event handling + arithmetic logic |
| [ApLab9](ApLab9/) | iNote | Notepad GUI, file I/O, object serialization |
| [ApLab10](ApLab10/) | Network, MultiThreadServer, MouseMover | TCP sockets, thread pools, AWT `Robot` |

There is no single deployable application. Labs are independent and can be compiled separately.

---

## Repository structure

```
AUT-AP-Lab/
├── README.md
├── ApLab2/Student/src/          # Student + Lab console app
├── ApLab3/
│   ├── ClockDisplay/src/
│   └── MusicOrganizer/src/
├── ApLab4/VotingSystem/src/     # includes JalaliCalendar-1.3.1.jar
├── ApLab5/
│   ├── BadPaint/src/            # separate type-specific collections
│   └── GoodPaint/src/           # Shape → Polygon hierarchy
├── ApLab6/                      # CRC card PDFs only
├── ApLab7/Calculator/src/       # UI-only calculator
├── ApLab8/Calculator/src/       # calculator with operators + listeners
├── ApLab9/iNote/src/            # packages: gui, model, utils
└── ApLab10/
    ├── Network/src/             # single-connection TCP echo-style server
    ├── MultiThreadServer/src/   # ExecutorService-based server
    └── MouseMover/src/
```

Each lab README describes that session’s purpose, classes, how to run it, and known limitations.

---

## Requirements

- A JDK that can compile the sources (projects use Java SE APIs; ApLab9 uses `InputStream.readAllBytes()`, which needs **Java 9+**)
- For GUI labs (7–9, MouseMover): a desktop environment that supports Swing/AWT
- ApLab4: the bundled `JalaliCalendar-1.3.1.jar` on the classpath

No Maven, Gradle, or IDE project files are included.

---

## How to compile and run

From a lab’s `src` directory (adjust paths as needed):

```bash
# Typical console lab (no packages)
javac *.java
java Main          # or Run, depending on the entry class

# ApLab4 (external JAR)
javac -cp "JalaliCalendar-1.3.1.jar:." *.java
java -cp "JalaliCalendar-1.3.1.jar:." Main

# ApLab9 (packages under src/)
javac Main.java gui/*.java model/*.java utils/*.java
java Main

# ApLab10 Network — start server first, then client
javac Server.java Client.java
java Server        # terminal 1
java Client        # terminal 2
```

On Windows, replace classpath `:` with `;`.

Entry classes are listed in each lab’s README.

---

## Skills demonstrated

Concrete implementation work across the labs includes:

- **OOP:** classes, constructors, getters/setters, composition (`ClockDisplay` + `NumberDisplay`)
- **Collections:** arrays, `ArrayList`, `HashMap`, `HashSet`, iterators
- **Inheritance & polymorphism:** `Shape` / `Polygon` hierarchy in GoodPaint vs. duplicated APIs in BadPaint
- **GUI:** Swing (`JFrame`, `JTabbedPane`, menus, listeners), Nimbus look-and-feel
- **I/O:** buffered readers/writers, byte streams, Java object serialization
- **Networking & concurrency:** `ServerSocket` / `Socket`, `ExecutorService` thread pool
- **Design artifacts:** CRC cards (ApLab6) for Health System and Theatre scenarios

---

## Limitations (repository-wide)

- No automated tests, CI, or dependency management
- Several programs are educational demos (e.g. music “playback” prints messages; ApLab7 buttons have no listeners)
- Some platform-specific behavior (ClockDisplay clears the console with Windows `cmd /c cls`)
- ApLab6 contains design PDFs only—no corresponding Java implementation

See individual lab READMEs for feature status (implemented / partial / UI-only).

---

## License

No license file is present in this repository. Treat the code as coursework unless the author states otherwise.
