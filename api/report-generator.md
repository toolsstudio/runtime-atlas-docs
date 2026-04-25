# Report Generator API

**Namespace:** `RuntimeAtlas.Editor`  
**Assembly:** `RuntimeAtlas.Editor`  
**Runtime Atlas v1.1.0**

---

## `RAReportGenerator` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class RAReportGenerator
```

Assembles session data from all monitored subsystems and writes it to disk in JSON, HTML, Markdown, or CSV format.

---

## `ReportData` class

```csharp
public sealed class ReportData
```

Holds the complete data set for one report. Populated by the report panel before export.

### Session Fields

| Member | Type | Description |
|--------|------|-------------|
| `ProjectName` | `string` | `Application.productName` |
| `UnityVersion` | `string` | `Application.unityVersion` |
| `Platform` | `string` | Active build target name |
| `Date` | `string` | ISO 8601 timestamp at report generation time |
| `SessionDuration` | `float` | Elapsed Play Mode time in seconds |
| `TotalFrames` | `int` | Number of profiler frames recorded |
| `AvgFPS` | `float` | Mean FPS across recorded frames |
| `MinFPS` | `float` | Minimum recorded FPS |
| `MaxFPS` | `float` | Maximum recorded FPS |
| `AvgMemoryMB` | `float` | Mean GC heap size in MB |
| `PeakMemoryMB` | `float` | Maximum recorded GC heap size in MB |
| `TotalAlerts` | `int` | Total alerts including dismissed |
| `CriticalAlerts` | `int` | Critical-severity alert count |
| `WarningAlerts` | `int` | Warning-severity alert count |
| `InfoAlerts` | `int` | Info-severity alert count |
| `ScannerIssues` | `int` | Total issues from the last scanner run |

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

```csharp
// Export as JSON. Returns the output file path on success, null on failure.
public string ExportJSON(ReportData data, string outputDirectory)

// Export as HTML. Returns the output file path on success, null on failure.
public string ExportHTML(ReportData data, string outputDirectory)

// Export as Markdown. Returns the output file path on success, null on failure.
public string ExportMarkdown(ReportData data, string outputDirectory)

// Export as CSV. Writes two files: session summary and frame data.
// Returns the summary file path on success, null on failure.
public string ExportCSV(ReportData data, string outputDirectory)
```

All methods are synchronous. File names are generated automatically using the format:

```
RuntimeAtlas_Report_YYYY-MM-DD_HH-mm-ss.[ext]
```

See [Report Export Guide](../guides/report-export.md) for format layout details.
