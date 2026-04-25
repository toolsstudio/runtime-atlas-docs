# Report Export

**Runtime Atlas v1.1.0**

---

## Overview

The Report tab generates a structured session report from live Runtime Atlas data and exports it to disk. Four formats are available. All formats capture the same underlying data set — the format choice affects layout and downstream usage, not content.

---

## Generating and Exporting

1. Open **Window > Runtime Atlas > Open** (`Ctrl+Alt+R`).
2. Select the **Report** tab.
3. Click **Generate Preview**. This assembles the `ReportData` object from the current session state.
4. Select an export format.
5. Click **Export**.
6. Choose a destination directory. The file is written synchronously. A confirmation message shows the output path.

Export can be triggered at any time. Data reflects the state at the moment **Generate Preview** is clicked, not at export time. Click **Generate Preview** again before exporting if you want a fresh snapshot.

---

## File Naming

All export files follow this naming convention:

```
RuntimeAtlas_Report_YYYY-MM-DD_HH-mm-ss.[ext]
```

For CSV exports, two files are written:

```
RuntimeAtlas_Report_YYYY-MM-DD_HH-mm-ss.csv          ← session summary
RuntimeAtlas_Report_YYYY-MM-DD_HH-mm-ss_Frames.csv   ← per-frame data
```

---

## Format Reference

### JSON

**Extension:** `.json`  
**Use case:** Programmatic processing, CI pipelines, custom tooling, data archiving.

The JSON output is a single object matching the `ReportData` structure. All fields are included. Arrays are fully populated.

```json
{
  "ProjectName": "MyGame",
  "UnityVersion": "6000.3.10f1",
  "Platform": "WindowsEditor",
  "Date": "2025-04-24T19:53:14",
  "SessionDuration": 120.4,
  "TotalFrames": 7200,
  "AvgFPS": 60.1,
  "MinFPS": 28.3,
  "MaxFPS": 168.0,
  "AvgMemoryMB": 64.2,
  "PeakMemoryMB": 91.7,
  "TotalAlerts": 6,
  "CriticalAlerts": 0,
  "WarningAlerts": 4,
  "InfoAlerts": 2,
  "ScannerIssues": 12,
  "Alerts": [
    {
      "Severity": "Warning",
      "Message": "Far/Near clip ratio 3333:1 — depth precision may degrade",
      "Source": "Camera",
      "Time": "19:53:22"
    }
  ],
  "ScanResults": [
    {
      "File": "Assets/Scripts/EnemyAI.cs",
      "Line": 47,
      "Issue": "FindObjectOfType<T> called outside Awake/Start",
      "Category": "Hot path",
      "Severity": "Warning"
    }
  ],
  "Frames": [
    { "Time": 0.0, "FPS": 60.2, "MemoryMB": 63.1 },
    { "Time": 0.016, "FPS": 61.0, "MemoryMB": 63.1 }
  ]
}
```

---

### HTML

**Extension:** `.html`  
**Use case:** Sharing with team members, attaching to bug reports, browser-readable summaries.

A self-contained HTML file with embedded CSS. No external dependencies. Opens in any modern browser.

**Sections:**

1. Header — project name, version, platform, date
2. Performance Summary — FPS range, average, session duration, memory range
3. Alert Summary — counts by severity, full alert list as a styled table
4. Scanner Summary — issue count, full result list as a styled table
5. Footer — Runtime Atlas version

---

### Markdown

**Extension:** `.md`  
**Use case:** Pasting into GitHub issues, Confluence pages, internal documentation, plain-text review.

The output is standard CommonMark. No HTML is embedded. All tables use GFM pipe syntax.

**Structure:**

```markdown
# Runtime Atlas Report — MyGame
**Date:** 2025-04-24  |  **Unity:** 6000.3.10f1  |  **Platform:** WindowsEditor

## Performance
| Metric | Value |
|--------|-------|
| Avg FPS | 60.1 |
...

## Alerts (6)
| Severity | Message | Source | Time |
|----------|---------|--------|------|
...

## Scanner Results (12)
| File | Line | Issue | Category | Severity |
|------|------|-------|----------|----------|
...
```

---

### CSV

**Extension:** `.csv` (two files)  
**Use case:** Spreadsheet import (Excel, Google Sheets, Numbers), data analysis, custom charting.

**Summary file columns:**

```
ProjectName, UnityVersion, Platform, Date, SessionDuration, TotalFrames,
AvgFPS, MinFPS, MaxFPS, AvgMemoryMB, PeakMemoryMB,
TotalAlerts, CriticalAlerts, WarningAlerts, InfoAlerts, ScannerIssues
```

One data row. Headers on the first row.

**Frames file columns:**

```
Time, FPS, MemoryMB
```

One row per recorded frame. Headers on the first row. This file can contain thousands of rows depending on session length and profiler capacity.

---

## Report Data Freshness

Report data captures the state at the moment **Generate Preview** is clicked:

- Profiler frame statistics are from the current buffer at that instant.
- Alerts include all alerts ever raised in the session, including dismissed ones.
- Scanner results are from the most recent scan run. If no scan has been run, `ScannerIssues` is `0` and `ScanResults` is empty.
- Timeline frame data and profiler frames are independent — the Report uses profiler frames, not timeline frames.
