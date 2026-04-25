# Console Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Captures Unity log messages that are tagged with a Runtime Atlas prefix and displays them in a filtered ring buffer. Provides a scoped view of logs emitted by Runtime Atlas-aware code without showing the full Unity Console.

---

## Log Tag Requirement

The Runtime Atlas Console only captures messages that begin with one of the following prefixes:

```
[RA]
[Runtime Atlas]
[RuntimeAtlas]
```

Messages without these prefixes are ignored. This is by design — the tab provides a focused diagnostic view, not a replacement for the Unity Console.

To emit a message that appears in the Runtime Atlas Console:

```csharp
Debug.Log("[RA] Camera FOV updated to 60");
Debug.LogWarning("[Runtime Atlas] High GC alloc detected");
Debug.LogError("[RuntimeAtlas] Missing AudioListener");
```

---

## Capture Controls

| Control | Action |
|---------|--------|
| **Start Capture** | Begin intercepting tagged log messages |
| **Stop Capture** | Stop intercepting. Existing buffer is preserved. |
| **Clear** | Empty the buffer |
| **Clear on Play** | When enabled, clears the buffer each time Play Mode starts |
| **Export .txt** | Writes the buffer to a plain text file |

Capture starts automatically when the window opens and Play Mode is entered.

---

## Filter Buttons

| Filter | Shows |
|--------|-------|
| **Log** | `Debug.Log` messages |
| **Warning** | `Debug.LogWarning` messages |
| **Error** | `Debug.LogError` and `Debug.LogException` messages |

Each filter button shows the count of messages of that type in the current buffer.

---

## Log Entry Fields

Each captured entry stores:

| Field | Description |
|-------|-------------|
| **Message** | Full log message text |
| **Stack trace** | Call stack at the time of logging |
| **Type** | Log, Warning, Error, or Exception |
| **Timestamp** | Editor time when the message was logged |
| **Source file** | Script file that called `Debug.Log` |
| **Source line** | Line number |
| **Repeat count** | Number of consecutive identical messages aggregated |
| **Dismissed** | Whether the entry has been dismissed |

---

## Ring Buffer

The Console uses a fixed-capacity ring buffer. When the buffer is full, the oldest entries are overwritten. Default capacity is 500 entries. This keeps memory usage bounded regardless of session length.

---

## Search

The search field filters the displayed list to entries whose message contains the search string. Search is case-insensitive.
