# Console Capture API

**Namespace:** `RuntimeAtlas.Editor`  
**Assembly:** `RuntimeAtlas.Editor`  
**Runtime Atlas v1.1.0**

---

## `ConsoleCapture` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class ConsoleCapture
```

Intercepts Unity log messages emitted with a Runtime Atlas prefix tag and stores them in a fixed-capacity ring buffer. Provides filtering, repeat aggregation, and plain-text export.

---

## Tag Requirement

Only messages that begin with one of the following prefixes are captured:

```
[RA]
[Runtime Atlas]
[RuntimeAtlas]
```

Messages without these prefixes are discarded.

---

## `LogEntry` class

```csharp
public sealed class LogEntry
```

| Member | Type | Description |
|--------|------|-------------|
| `Message` | `string` | Full message text including the prefix tag |
| `StackTrace` | `string` | Call stack at time of logging |
| `Type` | `LogType` | `Log`, `Warning`, `Error`, or `Exception` |
| `Timestamp` | `double` | Editor time when the message was received |
| `SourceFile` | `string` | Script file that called `Debug.Log` |
| `SourceLine` | `int` | Line number of the `Debug.Log` call |
| `Dismissed` | `bool` | Whether the user has dismissed this entry |
| `RepeatCount` | `int` | Number of consecutive identical messages aggregated into this entry |
| `DisplayTime` | `string` | Pre-formatted timestamp string for UI display |

---

## Configuration Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `ClearOnPlay` | `bool` | `true` | Clear buffer when Play Mode starts |
| `CaptureLog` | `bool` | `true` | Capture `LogType.Log` messages |
| `CaptureWarning` | `bool` | `true` | Capture `LogType.Warning` messages |
| `CaptureError` | `bool` | `true` | Capture `LogType.Error` messages |
| `CaptureException` | `bool` | `true` | Capture `LogType.Exception` messages |

---

## State Properties

| Property | Type | Description |
|----------|------|-------------|
| `IsCapturing` | `bool` | Whether the capture hook is active |
| `Count` | `int` | Number of entries currently in the buffer |
| `TotalCaptured` | `int` | Total messages captured since last clear |
| `LogCount` | `int` | Count of `Log`-type entries in buffer |
| `WarningCount` | `int` | Count of `Warning`-type entries in buffer |
| `ErrorCount` | `int` | Count of `Error` and `Exception` entries in buffer |

---

## Constructor

```csharp
public ConsoleCapture(AlertSystem alertSystem, int capacity = 500)
```

| Parameter | Description |
|-----------|-------------|
| `alertSystem` | The `AlertSystem` instance used to raise alerts on captured errors |
| `capacity` | Maximum number of log entries in the ring buffer. When full, the oldest entry is overwritten. |

---

## Methods

```csharp
// Register the Unity log handler. Safe to call multiple times.
public void StartCapture()

// Unregister the log handler. Buffer contents are preserved.
public void StopCapture()

// Clear all entries from the buffer and reset counters.
public void Clear()

// Retrieve an entry by logical index (0 = oldest).
public LogEntry GetEntry(int logicalIndex)

// Export the entire buffer as a plain-text string.
// Each entry is formatted as: [TIME] [TYPE] message
public string ExportAsText()
```
