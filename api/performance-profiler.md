# Performance Profiler API
**Runtime Atlas v1.2.0**

---

## Assembly

`RuntimeAtlas.Editor` | Namespace: `RuntimeAtlas.Editor`

---

## PerfSample

```csharp
public readonly struct PerfSample
{
    public int   Frame       { get; }
    public float FrameTimeMs { get; }
    public float FPS         { get; }
    public float GCHeapMB    { get; }
    public float GCAllocKB   { get; }
    public int   DrawCalls   { get; }
    public int   Triangles   { get; }
    public int   Vertices    { get; }
}
```

| Field | Source | Unit |
|-------|--------|------|
| `Frame` | `Time.frameCount` | — |
| `FrameTimeMs` | `Time.unscaledDeltaTime * 1000f` | ms |
| `FPS` | `1000f / FrameTimeMs` | fps |
| `GCHeapMB` | `GC.GetTotalMemory(false) / (1024f * 1024f)` | MB |
| `GCAllocKB` | Per-frame delta of `GC.GetTotalMemory` | KB |
| `DrawCalls` | `UnityStats.drawCalls` | — |
| `Triangles` | `UnityStats.triangles` | — |
| `Vertices` | `UnityStats.vertices` | — |

`PerfSample` is a `readonly struct`. It allocates no heap memory.

---

## PerformanceProfiler

```csharp
public sealed class PerformanceProfiler
```

**Reading samples:**

```csharp
public IReadOnlyList<PerfSample> Samples { get; }
public PerfSample Latest { get; }
```

`Samples` returns the full recorded ring buffer in chronological order (oldest first). `Latest` returns the most recent sample.

**Playback state:**

```csharp
public bool IsPaused { get; }
public void Pause();
public void Resume();
public void Clear();
```

**Configuration:**

```csharp
public int   MaxSamples         { get; set; }  // default: 300
public float WarnFrameTimeMs    { get; set; }  // default: 33.3f
public float CriticalFrameTimeMs{ get; set; }  // default: 50.0f
public float WarnGCAllocKB      { get; set; }  // default: 64f
```

Changing `MaxSamples` clears the existing sample buffer.

---

## Data Collection

`PerformanceProfiler.Poll()` is called on `EditorApplication.update` at up to 60 Hz. It is a zero-allocation hot path — `PerfSample` is a struct and the internal ring buffer is a fixed-size array reused across frames.

`UnityStats` values are only non-zero during Play Mode. In Edit Mode, `DrawCalls`, `Triangles`, and `Vertices` are zero.
