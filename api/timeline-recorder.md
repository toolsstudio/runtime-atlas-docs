# Timeline Recorder API
**Runtime Atlas v1.2.0**

---

## Assembly

`RuntimeAtlas.Editor` | Namespace: `RuntimeAtlas.Editor`

---

## FrameData

```csharp
public readonly struct FrameData
{
    public int   Frame        { get; }
    public float FrameTimeMs  { get; }
    public float FPS          { get; }
    public float GCHeapMB     { get; }
    public int   CameraCount  { get; }
    public int   SourceCount  { get; }
    public int   AlertCount   { get; }
}
```

| Field | Description |
|-------|-------------|
| `Frame` | `Time.frameCount` at capture time |
| `FrameTimeMs` | Frame duration in milliseconds |
| `FPS` | Instantaneous FPS |
| `GCHeapMB` | GC heap size in MB at capture |
| `CameraCount` | Active camera count at capture |
| `SourceCount` | Active audio source count at capture |
| `AlertCount` | Non-dismissed alert count at capture |

`FrameData` is a `readonly struct`. No heap allocation.

---

## TimelineRecorder

```csharp
public sealed class TimelineRecorder
```

**Reading frames:**

```csharp
public int              Count   { get; }
public int              Capacity{ get; }
public FrameData        this[int index] { get; }
```

`Count` is the number of recorded frames (0 to `Capacity`). `this[index]` accesses frames by index (0 = oldest, Count-1 = newest). The recorder is a circular buffer — once full, oldest frames are overwritten without resizing.

**Playback cursor:**

```csharp
public int  PlaybackIndex   { get; set; }
public bool IsPlaying       { get; }
public void Play();
public void Pause();
public void StepForward();
public void StepBackward();
```

`PlaybackIndex` is clamped to `[0, Count - 1]`. Setting it directly is equivalent to scrubbing the timeline slider.

**Lifecycle:**

```csharp
public void RecordFrame(FrameData frame);
public void Clear();
```

`RecordFrame` is called by `AtlasWindow` on each `EditorApplication.update` during Play Mode. It is zero-allocation.

**Configuration:**

```csharp
public int Capacity { get; set; }  // default: 300
```

Changing `Capacity` clears the buffer.
