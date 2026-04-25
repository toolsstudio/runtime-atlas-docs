# Scanner Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Scans all C# script files in `Assets/` for common code quality issues. The scan is triggered manually — it never runs automatically or on every frame.

---

## Running a Scan

1. Open the **Scanner** tab.
2. Click **Scan Scripts**.
3. Wait for completion. Scan time scales with project size.
4. Review results in the list.

The tab shows the last scan time and the number of files scanned.

---

## Detected Issues

| Category | Issue | Severity |
|----------|-------|----------|
| Hot path | `FindObjectOfType<T>()` called inside a method body (not `Awake`/`Start`) | Warning |
| Empty lifecycle | `Update()` with no body | Info |
| Empty lifecycle | `FixedUpdate()` with no body | Info |
| Empty lifecycle | `LateUpdate()` with no body | Info |
| Null safety | Method returning a reference type with no null check on result | Info |

Patterns are matched using regular expressions against raw source text. The scanner does not compile or execute code.

---

## Result Fields

Each result shows:

| Field | Description |
|-------|-------------|
| **File** | Asset-relative path to the script |
| **Line** | Line number of the issue |
| **Issue** | Human-readable description |
| **Category** | Issue category (Hot path, Empty lifecycle, Null safety) |
| **Severity** | Info, Warning, or Critical |
| **Open** button | Opens the file at the flagged line in the Scripts viewer |

---

## Limitations

- The scanner operates on source text, not compiled assemblies. It cannot detect issues that require semantic analysis.
- Files in `Editor/` folders are included in the scan.
- Generated files (e.g., code generation output) may produce false positives if they match issue patterns.

---

## Relationship to Optimizer

Scanner results feed directly into the **Optimizer** tab. The Optimizer produces actionable fix suggestions from scanner output. See [Optimizer Tab](optimizer.md).
