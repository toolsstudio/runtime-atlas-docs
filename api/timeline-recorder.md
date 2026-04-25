# Timeline Recorder API

**Namespace:** `RuntimeAtlas.Editor`  
**Assembly:** `RuntimeAtlas.Editor`  
**Runtime Atlas v1.1.0**

---

## `TimelineRecorder` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class TimelineRecorder
```

Records a circular buffer of per-frame snapshots during Play Mode. Snapshots capture a cross-section of monitored system state each frame. The buffer is preserved after recording stops, enabling post-session scrubbing in the Timeline tab.

---

## `FrameData` struct

```csharp
public struct FrameData
```

| Member | Type | Description |
|--------|------|-------------|
| `Timestamp` | `double` | Editor time in seconds when this frame was recorded |
| `FPS` | `float` | Frames per second at this sample |
| `MemoryMB` | `float` | GC heap size in megabytes |
| `ActiveCameras` | `int` | Number of active `Camera` components this frame |
| `PlayingAudio` | `int` | Number of actively playing `AudioSource` components |
| `AlertCount` | `int` | Total non-dismissed alert count this frame |
| `CameraFOV` | `float` | FOV of the first active camera (degrees) |
| `MaxAudioVolume` | `float` | Volume of the loudest actively playing audio source |

---

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `IsRecording` | `bool` | Whether the recorder is currently active |
| `FrameCount` | `int` | Number of frames currently in the buffer |
| `BufferCapacity` | `int` | Maximum frames the buffer can hold |
| `ElapsedTime` | `double` | Seconds elapsed since recording started. `0` if not recording. |
| `StartTime` | `double` | Editor time at which recording began |
| `LastFPS` | `float` | FPS value from the most recently recorded frame |

---

## Methods

```csharp
// Starts recording. Reallocates the buffer if capacity settings changed.
// Clears any existing buffer contents.
public void Start()

// Stops recording. Buffer contents are preserved for playback.
public void Stop()

// Stops recording and clears all buffered frames.
public void Reset()

// Records one frame into the circular buffer.
// Called automatically by the Timeline system each editor update.
// Not intended for direct call from user code.
public void RecordFrame(
    CameraInspectorNode cameraNode,
    AudioInspectorNode  audioNode,
    AlertSystem         alertSystem,
    PerformanceProfiler profiler)

// Returns the frame at the given logical index.
// Index 0 is the oldest frame; index FrameCount-1 is the most recent.
public FrameData GetFrame(int index)
```

---

## Circular Buffer Behaviour

The recorder uses a fixed-size circular buffer. When the buffer is full, new frames overwrite the oldest. The `FrameCount` property reports the current number of valid frames, which equals `BufferCapacity` once the buffer has filled at least once.

Buffer capacity is configured in the Runtime Atlas settings panel.

---

## Usage in Reports

Timeline frame data is included in session report exports. Each frame appears as an entry in the `Frames` array of the `ReportData` structure. See [Report Generator API](report-generator.md).
