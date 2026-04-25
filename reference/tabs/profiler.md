# Profiler Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Records frame-accurate performance counters during Play Mode and displays them as a live scrolling graph. Designed for zero heap allocation in the hot recording path.

---

## Recorded Counters

Each frame sample captures:

| Counter | Description |
|---------|-------------|
| **Frame time (ms)** | Duration of the frame in milliseconds |
| **FPS** | Frames per second (`1000 / FrameMS`) |
| **GC heap (MB)** | Total managed heap size at time of sample |
| **GC alloc delta (bytes)** | Change in heap allocation since the previous sample |
| **Draw calls** | Number of draw calls (batches) this frame |
| **Triangles** | Total triangles rendered |
| **Vertices** | Total vertices rendered |
| **SetPass calls** | Number of shader pass changes |

---

## Thresholds and Spike Detection

Each sample is flagged against configurable thresholds:

| Threshold | Default | Meaning |
|-----------|---------|---------|
| Slow frame | 33.3 ms (~30 FPS) | Frame flagged `IsSlowFrame` |
| Critical frame | 50 ms (~20 FPS) | Alert raised after N consecutive slow frames |
| GC spike | 16 KB per sample | Frame flagged `IsGCSpike` |
| GC warning | 64 KB per sample | Warning-level alert |
| GC critical | 256 KB per sample | Critical-level alert |
| Slow frame alert count | 5 consecutive frames | Alert trigger threshold |
| Alert cooldown | 2 seconds | Minimum interval between repeated profiler alerts |

Thresholds are displayed and editable in the Profiler settings panel (⚙ icon).

---

## Graph Display

The graph shows the last N samples as a scrolling line chart. Slow frames are highlighted. GC spikes are marked as vertical indicators.

**Y-axis**: Frame time in ms (primary), GC alloc delta (secondary overlay)  
**X-axis**: Frame index (most recent on the right)

---

## Controls

| Control | Action |
|---------|--------|
| **Start / Stop** | Begin or end recording. Recording starts automatically on Play Mode entry. |
| **Reset** | Clear all samples and restart. |
| **Export CSV** | Write the current sample buffer to a CSV file via the Report system. |

---

## Relationship to the Report

Profiler frame data is included in the `Frames` array of exported session reports. See [Report Export](../../guides/report-export.md).
