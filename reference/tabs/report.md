# Report Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Generates a session report from the current Runtime Atlas data and exports it to a file. Reports include project metadata, frame statistics, all alerts, and all scanner results.

---

## Generating a Report

1. Click **Generate Preview**. The report is assembled from the current session state.
2. Review the preview in the text area.
3. Select an export format: JSON / HTML / Markdown / CSV / DOCX.
4. Click **Export** and choose a destination folder.

The file is written immediately. The export path is logged in the Unity Console.

---

## Export Formats

| Format | File extension | Use case |
|--------|---------------|---------|
| JSON | `.json` | Machine-readable; import into other tools |
| HTML | `.html` | Human-readable report with formatting |
| Markdown | `.md` | Documentation embedding |
| CSV | `.csv` | Spreadsheet import |
| DOCX | `.docx` | Word-compatible deliverable |
| XML | `.xml` | Structured data interchange |
| YAML | `.yml` | Config-style data |

See [Report Export](../../guides/report-export.md) for a full field reference per format.

---

## Report Data Structure

| Field | Source |
|-------|--------|
| Project name | `Application.productName` |
| Company | `Application.companyName` |
| Unity version | `Application.unityVersion` |
| Platform | `Application.platform` |
| Runtime Atlas version | `k_Version` constant |
| Session duration | Time from Play Mode entry to report generation |
| Camera snapshots | `CameraInspectorNode` snapshot list |
| Audio snapshots | `AudioInspectorNode` snapshot list |
| Alerts | `AlertSystem` log at generation time |
| Scanner results | `ScriptScanner` results at generation time |
| Performance samples | `PerformanceProfiler` recorded samples |
