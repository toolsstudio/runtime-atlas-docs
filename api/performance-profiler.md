# Performance Profiler API

**Namespace:** `RuntimeAtlas.Editor`  
**Assembly:** `RuntimeAtlas.Editor`  
**Runtime Atlas v1.2.0**

---

## `PerformanceProfiler` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class PerformanceProfiler
```

Frame-accurate performance sampler. Records FPS, frame time, GC heap size, GC allocation delta, and rendering statistics per frame. Zero heap allocations in the hot recording path.

Implements `IAlertSource`. Alerts are raised when consecutive slow frames or GC thresholds are exceeded.

---

## Constructor

```csharp
public PerformanceProfiler(AlertSystem alertSystem)
```

---

## `PerfSample` struct

```csharp
public struct PerfSample
```

| Member | Type | Description |
|--------|------|-------------|
| `Timestamp` | `double` | Editor time (seconds) when the sample was taken |
| `FrameMS` | `float` | Frame duration in milliseconds |
| `FPS` | `float` | Frames per second (`1000 / FrameMS`) |
| `GCMemMB` | `float` | GC heap size in megabytes |
| `GCAllocDelta` | `long` | Change in heap allocation since the previous sample (bytes) |
| `DrawCalls` | `int` | Draw call count (batches) this frame |
| `Triangles` | `int` | Total rendered triangles |
| `Vertices` | `int` | Total rendered vertices |
| `SetPassCalls` | `int` | Shader pass change count |
| `IsGCSpike` | `bool` | True if `GCAllocDelta > GCSpikeThresholdBytes` |
| `IsSlowFrame` | `bool` | True if `FrameMS > SlowFrameThresholdMS` |

---

## Configurable Thresholds

All thresholds are read from `RuntimeAtlasSettings` and take effect on the next recorded frame.

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `SlowFrameThresholdMS` | `float` | `33.3` | Frame time (ms) above which a frame is `IsSlowFrame` |
| `CriticalFrameThresholdMS` | `float` | `50.0` | Frame time (ms) for critical slow-frame alert |
| `GCSpikeThresholdBytes` | `long` | `16384` | GC alloc delta (bytes) that triggers `IsGCSpike` |
| `GCWarningThresholdBytes` | `long` | `65536` | GC alloc delta for Warning-level alert |
| `GCCriticalThresholdBytes` | `long` | `262144` | GC alloc delta for Critical-level alert |
| `SlowFrameAlertCount` | `int` | `5` | Consecutive slow frames before an alert fires |
| `AlertCooldownSeconds` | `double` | `2.0` | Minimum interval between repeated profiler alerts |

---

## State Properties

| Property | Type | Description |
|----------|------|-------------|
| `IsRunning` | `bool` | Whether recording is active |
| `SampleCount` | `int` | Number of valid samples in the buffer |
| `Capacity` | `int` | Maximum buffer capacity |
| `AvgFPS` | `float` | Mean FPS across all recorded samples |
| `MinFPS` | `float` | Minimum recorded FPS |
| `MaxFPS` | `float` | Maximum recorded FPS |
| `AvgFrameMS` | `float` | Mean frame time in milliseconds |

---

## Methods

```csharp
// Begin recording. Clears any existing buffer.
public void Start()

// Stop recording. Buffer is preserved.
public void Stop()

// Stop recording and clear all samples.
public void Reset()

// Record one frame. Called once per editor update during Play Mode.
// Zero allocations in this path.
public void Poll()

// Retrieve a sample by index. 0 = oldest in the circular buffer.
public PerfSample GetSample(int index)
```
