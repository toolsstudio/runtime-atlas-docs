# Scanner Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Scans all C# script files in `Assets/` for common code quality issues. Results feed the Optimizer tab and can be included in exported session reports. The scan is always manual — it never runs automatically.

---

## Running a Scan

1. Open the **Scanner** tab.
2. Click **Scan Scripts**.
3. Wait for completion. Scan time scales with project size.
4. Review results in the list. The tab header shows file count and issue count.

The last scan timestamp is displayed above the results.

---

## Detected Issue Patterns

| Category | Pattern | Severity |
|----------|---------|----------|
| Hot path | `FindObjectOfType<T>()` or `FindObjectsOfType<T>()` called inside any method other than `Awake` or `Start` | Warning |
| Empty lifecycle | `Update()`, `FixedUpdate()`, or `LateUpdate()` with no body | Info |
| Null safety | Method returning a reference type with no null check on the returned value at call sites | Info |

Pattern matching operates on raw source text via regular expressions. The scanner does not compile or execute code and cannot perform semantic analysis.

---

## Result Row Fields

| Field | Description |
|-------|-------------|
| **File** | Asset-relative path to the script |
| **Line** | Line number of the matched pattern |
| **Issue** | Human-readable issue description |
| **Category** | Hot path, Empty lifecycle, or Null safety |
| **Severity** | Info, Warning, or Critical |
| **Open** | Opens the Scripts tab at the flagged line |

---

## Excluding Paths

Paths can be excluded in Project Settings under `ScannerExcludePaths`. Entries are prefix-matched against the asset-relative path.

Example: adding `Assets/ThirdParty` excludes all files under that directory.

---

## Limitations

- Regex-based; cannot detect multi-file or context-dependent patterns.
- Files inside `Editor/` folders are included unless excluded via settings.
- Code-generated files may produce false positives if they match issue patterns.

---

## Relationship to Optimizer

Scanner results are the sole input to the Optimizer tab. Re-running the scan refreshes the Optimizer automatically. See [Optimizer tab](optimizer.md).
