# Console Capture API
**Runtime Atlas v1.2.0**

---

## Assembly

`RuntimeAtlas.Editor` | Namespace: `RuntimeAtlas.Editor`

---

## LogEntry

```csharp
public sealed class LogEntry
{
    public string    Message    { get; }
    public string    StackTrace { get; }
    public LogType   Type       { get; }
    public int       Frame      { get; }
}
```

| Property | Description |
|----------|-------------|
| `Message` | Full log message text |
| `StackTrace` | Stack trace string from Unity |
| `Type` | `LogType.Log`, `LogType.Warning`, or `LogType.Error` |
| `Frame` | `Time.frameCount` at capture time |

---

## ConsoleCapture

```csharp
public sealed class ConsoleCapture
```

**Reading entries:**

```csharp
public IReadOnlyList<LogEntry> Entries { get; }
```

Returns all captured entries, oldest first. The list reflects the ring buffer contents at read time.

**Lifecycle:**

```csharp
public void Clear();
```

Removes all captured entries.

**Configuration:**

```csharp
public int Capacity { get; set; }  // default: 500
```

Changing `Capacity` clears the buffer.

---

## Capture Rules

`ConsoleCapture` registers with `Application.logMessageReceived` and captures messages whose text begins with any of:

- `[RA]`
- `[RuntimeAtlas]`
- `[Runtime Atlas]`

Prefix matching is case-sensitive. Messages without a matching prefix are passed through to the Unity Console but not captured by Runtime Atlas.

---

## Ring Buffer Behaviour

The buffer is fixed-size (default 500). When full, the oldest entry is overwritten without reallocation.

---

## Usage in Own Code

```csharp
// These messages appear in both the Unity Console and the Runtime Atlas Console tab:
Debug.Log("[RA] Initialising subsystem");
Debug.LogWarning("[RuntimeAtlas] Threshold exceeded: 45 ms");
Debug.LogError("[Runtime Atlas] Null reference in AudioNode");
```
