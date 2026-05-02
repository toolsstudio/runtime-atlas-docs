# Timeline Recorder API

**Namespace:** `RuntimeAtlas.Editor`  
**Assembly:** `RuntimeAtlas.Editor`  
**Runtime Atlas v1.2.0**

---

## `TimelineRecorder` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class TimelineRecorder
```

Records a circular buffer of per-frame cross-system snapshots during Play Mode. The buffer is preserved after recording stops, enabling post-session scrubbing in the Timeline tab.

---

## Constructor

```csharp
public TimelineRecorder(AlertSystem alertSystem)
```

---

## `FrameData` struct

```csharp
public struct FrameData
```

| Member | Type | Description |
|--------|------|-------------|
| `Timestamp` | `double` | Editor time (seconds) when this frame was recorded |
| `FPS` | `float` | Frames per second at this sample |
| `MemoryMB` | `float` | GC heap size in megabytes |
| `ActiveCameras` | `int` | Active `Camera` components this frame |
| `PlayingAudio` | `int` | Actively playing `AudioSource` components |
| `AlertCount` | `int` | Total non-dismissed alert count this frame |
| `CameraFOV` | `float` | FOV of the first active camera (degrees) |
| `MaxAudioVolume` | `float` | Volume of the loudest actively playing audio source |

---

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `IsRecording` | `bool` | Whether the recorder is active |
| `FrameCount` | `int` | Number of valid frames currently in the buffer |
| `BufferCapacity` | `int` | Maximum frames the buffer can hold |
| `ElapsedTime` | `double` | Seconds elapsed since recording started. `0` when not recording. |
| `StartTime` | `double` | Editor time at which recording began |
| `LastFPS` | `float` | FPS from the most recently recorded frame |

---

## Methods

```csharp
// Start recording. Clears any existing buffer.
public void Start()

// Stop recording. Buffer contents are preserved for playback.
public void Stop()

// Stop recording and clear all buffered frames.
public void Reset()

// Record one frame. Called automatically each editor update during Play Mode.
// Not intended for direct call from user code.
public void RecordFrame(
    CameraInspectorNode cameraNode,
    AudioInspectorNode  audioNode,
    AlertSystem         alertSystem)

// Return the frame at the given logical index.
// 0 = oldest frame; FrameCount-1 = most recent.
public FrameData GetFrame(int index)
```

---

## Circular Buffer Behaviour

When the buffer is full, new frames overwrite the oldest. `FrameCount` equals `BufferCapacity` once the buffer has filled at least once. Buffer capacity is set via `TimelineBufferSize` in Project Settings.

---

## Stats Bar

The **Frame** field in the stats bar shows `TimelineRecorder.FrameCount` — the number of valid frames in the buffer, not `Time.frameCount`.
