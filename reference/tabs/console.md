# Console Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Captures Unity log messages tagged with a Runtime Atlas prefix and stores them in a fixed-capacity ring buffer. Provides a scoped diagnostic view separate from the full Unity Console.

---

## Tag Requirement

Only messages beginning with one of these prefixes are captured:

```
[RA]
[Runtime Atlas]
[RuntimeAtlas]
```

Messages without these prefixes are discarded. This is by design — the tab provides a focused diagnostic view, not a full Console mirror.

```csharp
// Captured
Debug.Log("[RA] Camera FOV updated to 60");
Debug.LogWarning("[Runtime Atlas] High GC alloc detected");
Debug.LogError("[RuntimeAtlas] Missing AudioListener");

// Not captured
Debug.Log("Player took damage");
```

---

## Controls

| Control | Action |
|---------|--------|
| **Start Capture** | Register the log intercept hook |
| **Stop Capture** | Unregister the hook. Buffer is preserved. |
| **Clear** | Empty the buffer and reset counters |
| **Clear on Play** | When enabled, clears the buffer at each Play Mode entry |
| **Export .txt** | Write the buffer to a plain-text file |

Capture starts automatically when the Runtime Atlas window opens.

---

## Filters

| Filter | Shows |
|--------|-------|
| **Log** | `Debug.Log` messages |
| **Warning** | `Debug.LogWarning` messages |
| **Error** | `Debug.LogError` and `Debug.LogException` messages |

Each filter button shows the count of that type in the current buffer.

---

## Log Entry Fields

| Field | Description |
|-------|-------------|
| **Message** | Full text including the prefix tag |
| **Stack trace** | Call stack at log time |
| **Type** | Log, Warning, Error, or Exception |
| **Timestamp** | Editor time when the message was received |
| **Source file** | Script that called `Debug.Log` |
| **Source line** | Line number of the `Debug.Log` call |
| **Repeat count** | Consecutive identical messages aggregated into one entry |
| **Dismissed** | Whether the user has dismissed this entry |

---

## Ring Buffer

Fixed-capacity. When full, the oldest entry is overwritten. Default capacity: 500 entries. Bounded memory use regardless of session length.

---

## Search

The search field filters the visible list to entries whose message contains the search string. Case-insensitive.
