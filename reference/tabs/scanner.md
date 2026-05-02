# Scanner Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Performs static analysis on C# source files in the configured search path. Detects common performance and code quality issues without requiring compilation or Play Mode.

---

## Running a Scan

1. Set the search path (defaults to `Assets/`).
2. Click **Scan Scripts**.
3. Wait for the scan to complete. Progress is shown in the button label.
4. Review results in the result list.

The scan is synchronous. On large projects (thousands of files) it may cause a brief editor pause. This is a known limitation.

---

## Detected Pattern Categories

| Category | Examples |
|----------|---------|
| Hot-path allocation | `new` inside `Update` / `FixedUpdate` / `LateUpdate` |
| Uncached `GetComponent` | `GetComponent<T>()` result not stored in a variable |
| `FindObjectsOfType` | Any call to find-all-objects methods |
| `Camera.main` in hot path | `Camera.main` accessed inside `Update` |
| `SendMessage` usage | `SendMessage` / `BroadcastMessage` calls |
| `Debug.Log` in hot path | Log calls inside `Update`-family methods |
| `Resources.Load` | Any `Resources.Load` call |
| `print()` usage | `print()` calls (slower than `Debug.Log`) |
| Unscaled transform access in loop | `transform.position` inside `for`/`foreach` without caching |

---

## Result Row Fields

| Field | Description |
|-------|-------------|
| File | Source file path (relative to `Assets/`) |
| Line | Line number |
| Issue | Human-readable description |
| Category | Issue category |
| Severity | Info / Warning / Critical |

Clicking the file path opens the file in the Scripts tab at the relevant line.

---

## Controls

| Control | Action |
|---------|--------|
| **Scan Scripts** | Run the scan |
| **Clear** | Clear all results |
| Search field | Filter results by file name or issue text |
| Severity filter | Show/hide results by severity level |

---

## Relationship to Optimizer Tab

The Optimizer tab reads the Scanner results and presents human-readable fix suggestions grouped by category. The Scanner must be run before the Optimizer shows data.
