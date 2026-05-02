# Report Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Assembles current session data into a structured report and writes it to disk. Five export formats are available. Data reflects the state at the moment **Generate Preview** is clicked.

---

## Workflow

1. Open the **Report** tab.
2. Click **Generate Preview** — assembles the `ReportData` object from current session state.
3. Review the summary in the preview panel.
4. Select an export format.
5. Click **Export** and choose a destination folder.

Export can be triggered at any time — during Play Mode or after. Click **Generate Preview** again before exporting if you need a fresh snapshot.

---

## Report Contents

| Section | Description |
|---------|-------------|
| **Project name** | `Application.productName` |
| **Unity version** | `Application.unityVersion` |
| **Platform** | Active build target name |
| **Date** | ISO 8601 timestamp at preview generation time |
| **Session duration** | Elapsed Play Mode time in seconds |
| **Total frames** | Profiler frames recorded |
| **Avg / Min / Max FPS** | FPS statistics across recorded profiler frames |
| **Avg / Peak memory (MB)** | GC heap statistics across recorded profiler frames |
| **Total alerts** | All alerts ever raised this session (including dismissed) |
| **Alert breakdown** | Critical / Warning / Info counts |
| **Scanner issues** | Total from the most recent scan (0 if no scan has been run) |
| **Alert list** | All individual alerts with severity, message, source, and time |
| **Scan results** | All scanner results with file, line, issue, category, and severity |
| **Frame data** | Per-frame FPS, memory, and timestamp (JSON and CSV only) |

---

## Export Formats

| Format | Extension | Best for |
|--------|-----------|---------|
| JSON | `.json` | Programmatic processing, CI pipelines, custom tooling |
| HTML | `.html` | Sharing with team members, browser-viewable summaries |
| Markdown | `.md` | GitHub issues, Confluence, plain-text review |
| CSV | `.csv` | Spreadsheet import, data analysis |
| DOCX | `.docx` | Formal deliverables, offline review |

CSV exports write two files: a session summary file and a per-frame data file.

See [Report Export Guide](../../guides/report-export.md) for format layout details and field mapping.

---

## File Naming

```
RuntimeAtlas_Report_YYYY-MM-DD_HH-mm-ss.[ext]
```

CSV second file:

```
RuntimeAtlas_Report_YYYY-MM-DD_HH-mm-ss_Frames.csv
```
