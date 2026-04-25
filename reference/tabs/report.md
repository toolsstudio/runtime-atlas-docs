# Report Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Assembles current session data into a structured report and exports it in one of four formats. Reports capture the state of all monitored subsystems at the time of generation.

---

## Generating a Report

1. Open the **Report** tab.
2. Click **Generate Preview** to assemble the report data.
3. The preview panel shows the report summary.
4. Select an export format.
5. Click **Export**.
6. Choose a destination folder. The file is written immediately.

Reports can be generated at any time — during Play Mode or after. Data reflects the most recent recorded state.

---

## Report Contents

| Section | Description |
|---------|-------------|
| **Project name** | Unity project name |
| **Unity version** | Unity Editor version |
| **Platform** | Current build target platform |
| **Date** | Export timestamp |
| **Session duration** | Elapsed Play Mode time in seconds |
| **Total frames** | Frame count recorded |
| **Average FPS** | Mean FPS across all recorded samples |
| **Min / Max FPS** | Minimum and maximum recorded FPS |
| **Average memory (MB)** | Mean GC heap size |
| **Peak memory (MB)** | Maximum recorded GC heap size |
| **Total alerts** | All alerts (including dismissed) |
| **Critical / Warning / Info counts** | Alert breakdown by severity |
| **Scanner issues** | Total issue count from the last scan |
| **Alert list** | All individual alerts with severity, message, source, and time |
| **Scan results** | All scanner results with file, line, issue, category, and severity |
| **Frame data** | Per-frame FPS, memory, and time (included in JSON and CSV) |

---

## Export Formats

| Format | File extension | Use case |
|--------|---------------|----------|
| JSON | `.json` | Programmatic processing, CI integration |
| HTML | `.html` | Shareable report, browser viewing |
| Markdown | `.md` | Documentation, GitHub issues, plain text review |
| CSV | `.csv` | Spreadsheet import, data analysis |

See [Report Export Guide](../../guides/report-export.md) for format details and field mapping.
