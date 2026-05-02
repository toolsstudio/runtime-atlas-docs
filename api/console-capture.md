# Console Capture API

**Namespace:** `RuntimeAtlas.Editor`  
**Assembly:** `RuntimeAtlas.Editor`  
**Runtime Atlas v1.2.0**

---

## `ConsoleCapture` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class ConsoleCapture
```

Intercepts Unity log messages tagged with a Runtime Atlas prefix and stores them in a fixed-capacity ring buffer. Provides filtering, repeat aggregation, and plain-text export.

---

## Constructor

```csharp
public ConsoleCapture(AlertSystem alertSystem, int capacity = 500)
```

| Parameter | Description |
|-----------|-------------|
| `alertSystem` | `AlertSystem` instance used to raise alerts on captured error-level messages |
| `capacity` | Ring buffer capacity. Oldest entries overwritten when full. |

---

## Tag Requirement

Only messages beginning with these prefixes are captured:

```
[RA]
[Runtime Atlas]
[RuntimeAtlas]
```

All other messages are discarded.

---

## `LogEntry` class

```csharp
public sealed class LogEntry
```

| Member | Type | Description |
|--------|------|-------------|
| `Message` | `string` | Full message text including the prefix tag |
| `StackTrace` | `string` | Call stack at log time |
| `Type` | `LogType` | `Log`, `Warning`, `Error`, or `Exception` |
| `Timestamp` | `double` | Editor time when the message was received |
| `SourceFile` | `string` | Script file that called `Debug.Log` |
| `SourceLine` | `int` | Line number of the `Debug.Log` call |
| `Dismissed` | `bool` | Whether the entry has been dismissed |
| `RepeatCount` | `int` | Consecutive identical messages aggregated into this entry |
| `DisplayTime` | `string` | Pre-formatted timestamp string for UI rendering |

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
| `IsCapturing` | `bool` | Whether the log intercept hook is registered |
| `Count` | `int` | Number of entries currently in the buffer |
| `TotalCaptured` | `int` | Total messages captured since last clear |
| `LogCount` | `int` | Count of `Log`-type entries in buffer |
| `WarningCount` | `int` | Count of `Warning`-type entries in buffer |
| `ErrorCount` | `int` | Count of `Error` and `Exception` entries in buffer |

---

## Methods

```csharp
// Register the Unity log handler. Safe to call when already registered.
public void StartCapture()

// Unregister the log handler. Buffer contents are preserved.
public void StopCapture()

// Clear all entries from the buffer and reset counters.
public void Clear()

// Retrieve an entry by logical index (0 = oldest).
public LogEntry GetEntry(int logicalIndex)

// Export the entire buffer as a plain-text string.
// Format per entry: [TIME] [TYPE] message
public string ExportAsText()
```
