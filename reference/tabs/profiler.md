# Profiler Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Records frame-accurate performance counters during Play Mode and displays them as a scrolling live graph. The hot recording path contains zero heap allocations.

---

## Recorded Counters

Each `PerfSample` captures:

| Counter | Description |
|---------|-------------|
| **Frame time (ms)** | Duration of the frame in milliseconds |
| **FPS** | Frames per second (`1000 / FrameMS`) |
| **GC heap (MB)** | Total managed heap size at sample time |
| **GC alloc delta (bytes)** | Change in heap allocation since the previous sample |
| **Draw calls** | Number of draw call batches this frame |
| **Triangles** | Total triangles rendered |
| **Vertices** | Total vertices rendered |
| **SetPass calls** | Number of shader pass changes |

---

## Spike Detection Flags

Each sample is annotated with boolean flags derived from configurable thresholds:

| Flag | Condition |
|------|-----------|
| `IsSlowFrame` | `FrameMS > SlowFrameThresholdMS` |
| `IsGCSpike` | `GCAllocDelta > GCSpikeThresholdBytes` |

---

## Default Thresholds

| Threshold | Default | Configurable |
|-----------|---------|-------------|
| Slow frame | 33.3 ms (≈ 30 FPS) | Yes — `SlowFrameThresholdMS` |
| Critical frame | 50 ms (≈ 20 FPS) | Yes — `CriticalFrameThresholdMS` |
| GC spike | 16 KB/frame | Yes — `GCSpikeThresholdBytes` |
| GC warning alert | 64 KB/frame | Yes — `GCWarningThresholdBytes` |
| GC critical alert | 256 KB/frame | Yes — `GCCriticalThresholdBytes` |
| Slow frame alert trigger | 5 consecutive frames | Yes — `SlowFrameAlertCount` |
| Alert cooldown | 2 seconds | Yes — `AlertCooldownSeconds` |

See [Settings Reference](../settings.md) for descriptions of each threshold.

---

## Graph Display

- **Y-axis (primary):** Frame time in ms
- **Y-axis (secondary overlay):** GC alloc delta
- **X-axis:** Frame index, most recent on the right
- Slow frames: highlighted background
- GC spikes: vertical marker indicators

---

## Controls

| Control | Action |
|---------|--------|
| **Start** | Begin recording. Starts automatically on Play Mode entry. |
| **Stop** | Pause recording. Buffer is preserved. |
| **Reset** | Stop recording and clear all samples. |
| **Export CSV** | Write the sample buffer to CSV via the Report system. |

---

## Alerts Generated

| Condition | Severity |
|-----------|----------|
| `SlowFrameAlertCount` consecutive frames above `SlowFrameThresholdMS` | Warning |
| Any frame above `CriticalFrameThresholdMS` | Critical |
| GC alloc delta above `GCWarningThresholdBytes` | Warning |
| GC alloc delta above `GCCriticalThresholdBytes` | Critical |

Profiler alerts respect `AlertCooldownSeconds` to prevent alert spam.

---

## Report Relationship

Profiler frame data is the source of the `Frames` array in exported session reports. See [Report Generator API](../../api/report-generator.md).
