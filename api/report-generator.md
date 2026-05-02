# Report Generator API
**Runtime Atlas v1.2.0**

---

## Assembly

`RuntimeAtlas.Editor` | Namespace: `RuntimeAtlas.Editor`

---

## ReportData

```csharp
public sealed class ReportData
{
    public string              ProjectName      { get; set; }
    public string              CompanyName      { get; set; }
    public string              UnityVersion     { get; set; }
    public string              Platform         { get; set; }
    public string              RAVersion        { get; set; }
    public string              GeneratedAt      { get; set; }
    public float               SessionDuration  { get; set; }
    public List<CameraSnapshot>   Cameras       { get; set; }
    public List<AudioSnapshot>    AudioSources  { get; set; }
    public List<AlertEntry>       Alerts        { get; set; }
    public List<ScanResult>       ScannerResults{ get; set; }
    public List<PerfSample>       PerfSamples   { get; set; }
}
```

`ReportData` is populated by `RAReportGenerator.Collect()` and then passed to an export method.

---

## RAReportGenerator

```csharp
public sealed class RAReportGenerator
```

**Collecting data:**

```csharp
public ReportData Collect(
    CameraInspectorNode  cameraNode,
    AudioInspectorNode   audioNode,
    AlertSystem          alertSystem,
    ScriptScanner        scanner,
    PerformanceProfiler  profiler
);
```

Assembles a `ReportData` from the current state of all provided modules. Called by the Report tab when **Generate Preview** is clicked.

**Exporting:**

```csharp
public string ExportJSON    (ReportData data, string folderPath);
public string ExportHTML    (ReportData data, string folderPath);
public string ExportMarkdown(ReportData data, string folderPath);
public string ExportCSV     (ReportData data, string folderPath);
public string ExportDOCX    (ReportData data, string folderPath);
public string ExportXML     (ReportData data, string folderPath);
public string ExportYAML    (ReportData data, string folderPath);
```

Each method writes a file to `folderPath` and returns the full path of the written file. The filename is generated as `RuntimeAtlas_Report_<timestamp>.<ext>`.

Throws `System.IO.IOException` if the path is not writable.

---

## ExportFormat Enum

```csharp
public enum ExportFormat
{
    JSON,
    HTML,
    Markdown,
    CSV,
    DOCX,
    XML,
    YAML
}
```

Used by the Report tab UI to select the active format before calling Export.
