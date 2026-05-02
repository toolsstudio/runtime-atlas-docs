# Report Generator API

**Namespace:** `RuntimeAtlas.Editor`  
**Assembly:** `RuntimeAtlas.Editor`  
**Runtime Atlas v1.2.0**

---

## `RAReportGenerator` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class RAReportGenerator
```

Assembles session data from all monitored subsystems and writes it to disk in JSON, HTML, Markdown, CSV, or DOCX format.

---

## `ReportData` class

```csharp
public sealed class ReportData
```

Holds the complete data set for one report. Populated by `RAReportPanel` before export.

### Session Fields

| Member | Type | Description |
|--------|------|-------------|
| `ProjectName` | `string` | `Application.productName` |
| `UnityVersion` | `string` | `Application.unityVersion` |
| `Platform` | `string` | Active build target name |
| `Date` | `string` | ISO 8601 timestamp at preview generation time |
| `SessionDuration` | `float` | Elapsed Play Mode time in seconds |
| `TotalFrames` | `int` | Profiler frames recorded |
| `AvgFPS` | `float` | Mean FPS across recorded profiler frames |
| `MinFPS` | `float` | Minimum recorded FPS |
| `MaxFPS` | `float` | Maximum recorded FPS |
| `AvgMemoryMB` | `float` | Mean GC heap size in MB |
| `PeakMemoryMB` | `float` | Maximum recorded GC heap size in MB |
| `TotalAlerts` | `int` | All alerts including dismissed |
| `CriticalAlerts` | `int` | Critical-severity count |
| `WarningAlerts` | `int` | Warning-severity count |
| `InfoAlerts` | `int` | Info-severity count |
| `ScannerIssues` | `int` | Total issues from the most recent scan |

### Collections

| Member | Type | Description |
|--------|------|-------------|
| `Alerts` | `List<AlertExport>` | All alert entries |
| `ScanResults` | `List<ScanExport>` | All scanner results |
| `Frames` | `List<FrameExport>` | Per-frame performance samples |

---

## `AlertExport` struct

| Member | Type | Description |
|--------|------|-------------|
| `Severity` | `string` | `"Info"`, `"Warning"`, or `"Critical"` |
| `Message` | `string` | Alert message text |
| `Source` | `string` | Contributing system name |
| `Time` | `string` | Formatted timestamp |

---

## `ScanExport` struct

| Member | Type | Description |
|--------|------|-------------|
| `File` | `string` | Asset-relative script path |
| `Line` | `int` | Line number |
| `Issue` | `string` | Issue description |
| `Category` | `string` | Issue category |
| `Severity` | `string` | `"Info"`, `"Warning"`, or `"Critical"` |

---

## `FrameExport` struct

| Member | Type | Description |
|--------|------|-------------|
| `Time` | `float` | Timestamp in seconds |
| `FPS` | `float` | Frames per second |
| `MemoryMB` | `float` | GC heap size in MB |

---

## Export Methods

All methods are synchronous. File names follow:

```
RuntimeAtlas_Report_YYYY-MM-DD_HH-mm-ss.[ext]
```

Return value: output file path on success, `null` on failure.

```csharp
public string ExportJSON(ReportData data, string outputDirectory)

public string ExportHTML(ReportData data, string outputDirectory)

public string ExportMarkdown(ReportData data, string outputDirectory)

// Writes two files: session summary and frame data.
// Returns the summary file path.
public string ExportCSV(ReportData data, string outputDirectory)

public string ExportDOCX(ReportData data, string outputDirectory)
```

See [Report Export Guide](../guides/report-export.md) for per-format layout details and field mapping.
