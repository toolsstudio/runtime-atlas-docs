# Report Export
**Runtime Atlas v1.2.0**

---

## Overview

The Report tab generates a session report from Runtime Atlas data and exports it to a file. This guide documents the export workflow and the fields included in each format.

---

## Export Workflow

1. Open the **Report** tab.
2. Click **Generate Preview**. The report is assembled from current session state.
3. Review the preview in the text area.
4. Select a format (JSON, HTML, Markdown, CSV, DOCX, XML, or YAML).
5. Click **Export**.
6. Choose a destination folder. The file is written and the path is logged.

Generate Preview must be clicked before Export. Clicking Export on empty state produces an empty file.

---

## Report Data Fields

| Field | Source |
|-------|--------|
| `projectName` | `Application.productName` |
| `companyName` | `Application.companyName` |
| `unityVersion` | `Application.unityVersion` |
| `platform` | `Application.platform.ToString()` |
| `runtimeAtlasVersion` | `k_Version` constant in `AtlasWindow` |
| `generatedAt` | System time at Generate Preview click |
| `sessionDuration` | Time from Play Mode entry to report generation |
| `cameras[]` | Camera snapshot list from `CameraInspectorNode` |
| `audioSources[]` | Audio snapshot list from `AudioInspectorNode` |
| `alerts[]` | Alert log from `AlertSystem` at generation time |
| `scannerResults[]` | Script scanner results from `ScriptScanner` |
| `perfSamples[]` | Performance samples from `PerformanceProfiler` |

---

## Format Reference

### JSON

Structured JSON object matching the `ReportData` class. All fields present as documented above.

Best for: machine processing, importing into dashboards or custom tooling.

### HTML

Self-contained HTML file. Includes embedded CSS for readable formatting in any browser. Sections: project metadata, performance summary, camera list, audio list, alerts table, scanner results table.

Best for: sharing with non-technical stakeholders or archiving as a readable artifact.

### Markdown

GitHub-compatible Markdown. Uses standard ATX headers and fenced code blocks. Fields formatted as tables where applicable.

Best for: embedding in project wikis, README files, or issue trackers.

### CSV

Comma-separated values. Each row is one record. Multiple sections (camera, audio, alerts, scanner) are separated by blank rows with a section header comment.

Best for: importing into spreadsheets or data analysis tools.

### DOCX

Word-compatible `.docx` file. Uses `System.IO.Compression` to construct the Open XML format. Includes headers, tables, and body text. Does not require Microsoft Word to be installed.

Best for: formal deliverables or reports that need to be edited in Word.

### XML

Well-formed XML document. Root element `<RuntimeAtlasReport>` with child elements per section.

Best for: systems that consume XML.

### YAML

YAML 1.1 format. Indented structure matching the JSON schema.

Best for: config-adjacent tooling or human-readable structured data.
