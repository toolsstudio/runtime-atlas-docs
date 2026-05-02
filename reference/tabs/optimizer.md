# Optimizer Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Presents human-readable fix suggestions derived from Script Scanner results. Groups related issues and provides concrete recommended actions.

---

## Prerequisite

The Script Scanner must have been run at least once before this tab shows data. If no scan results are present, the tab shows a prompt to run the Scanner first.

---

## Suggestion Format

Each suggestion contains:

| Field | Description |
|-------|-------------|
| Category | Issue category (e.g., "Hot-path allocation") |
| Issue count | Number of scanner results in this category |
| Description | What the pattern is and why it is a problem |
| Fix recommendation | Concrete code-level action |
| Example | Before/after code snippet |

---

## Categories

| Category | Suggested Fix |
|----------|--------------|
| Hot-path allocation | Move `new` expressions outside the `Update` loop; use object pooling or pre-allocated arrays |
| Uncached `GetComponent` | Cache the result in `Awake` or `Start`; use a private field |
| `FindObjectsOfType` | Cache the result; refresh only when scene changes |
| `Camera.main` | Cache `Camera.main` in `Start`; `Camera.main` calls `FindObjectsOfType` internally |
| `SendMessage` | Replace with direct method calls or UnityEvents |
| `Debug.Log` in hot path | Remove or wrap in `#if UNITY_EDITOR` / conditional compilation |
| `Resources.Load` | Preload assets in `Awake`; avoid loading in hot paths |
| `print()` | Replace with `Debug.Log()` |

---

## Limitations

The Optimizer shows suggestions only for patterns the Scanner detected. It does not guarantee all performance issues in a project are covered. It does not execute any code changes — all actions are manual.
