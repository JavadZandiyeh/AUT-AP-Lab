# ApLab10 — Networking & Mouse Automation

Three small programs: a single-connection TCP server/client, a multithreaded TCP server with a matching client, and a utility that nudges the mouse cursor periodically.

Part of the [AUT AP Lab](../README.md) series.

---

## Projects

| Project | Entry classes | Port | Description |
|---------|---------------|------|-------------|
| [Network](#network) | `Server`, `Client` | `6000` | One client; cumulative echo-style responses |
| [MultiThreadServer](#multithreadserver) | `Server`, `Client` | `1000` | Cached thread pool; up to 10 accepted connections |
| [MouseMover](#mousemover) | `MouseMover` | — | Moves cursor slightly every 10 seconds |

---

## Network

### Behavior

1. `Server` listens on **localhost:6000**, accepts **one** connection.
2. Client sends lines from stdin as raw bytes.
3. Server appends each message (plus a space) to a `StringBuilder` and writes the **entire builder** back.
4. Client prints the response. Sending `over` ends the server’s read loop.

### Build and run

```bash
cd Network/src
javac *.java
# Terminal 1
java Server
# Terminal 2
java Client
```

Type messages in the client; type `over` to stop the server loop.

### Status

| Feature | Status |
|---------|--------|
| Blocking accept + single client | Implemented |
| Cumulative response buffer | Implemented |
| Multiple concurrent clients | Not supported (use MultiThreadServer) |

---

## MultiThreadServer

### Behavior

- `Server` binds **port 1000**, uses `Executors.newCachedThreadPool()`.
- Each accepted socket is handled by a `connectionHandler` `Runnable` (same accumulate-and-echo protocol as Network).
- Accepts at most **10** connections, then shuts down the pool (server process ends accepting; handlers may still finish).
- `Client` connects to `localhost:1000` (same client pattern as Network).

### Build and run

```bash
cd MultiThreadServer/src
javac *.java
java Server    # terminal 1
java Client    # terminal 2 (run multiple clients to exercise threads)
```

### Status

| Feature | Status |
|---------|--------|
| Per-connection thread via executor | Implemented |
| Shared protocol with Network (`over` to stop) | Implemented |
| Unlimited / long-running accept loop | Not implemented (hard cap of 10 accepts) |

---

## MouseMover

### Behavior

Uses `MouseInfo` for the current pointer location and `java.awt.Robot` to move the mouse by a small random offset (`±1`-style) every **10 seconds**, in an infinite loop.

### Build and run

```bash
cd MouseMover/src
javac MouseMover.java
java MouseMover
```

Stop with Ctrl+C. Needs a graphical session and OS permission for synthetic input where required.

### Status

| Feature | Status |
|---------|--------|
| Periodic small cursor moves | Implemented |
| Configurable interval / distance | Not implemented (hard-coded) |

---

## Technology stack

- `java.net.ServerSocket` / `Socket`
- `InputStream` / `OutputStream` with byte buffers
- `java.util.concurrent.ExecutorService`
- AWT `Robot`, `MouseInfo`, `Point`

---

## Limitations

- No framing protocol (message boundaries are raw TCP reads; partial reads possible).
- Servers are localhost demos without authentication or encryption.
- `connectionHandler` class name is package-private in `Server.java` (MultiThreadServer).
- MouseMover runs forever until interrupted; may be undesirable on shared machines.

---

## Related

- [Main README](../README.md)
- Previous: [ApLab9](../ApLab9/)
