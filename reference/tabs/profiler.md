# Profiler Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Records per-frame performance metrics. The tab contains a live graph and a scrollable sample list. Data is collected at up to 60 Hz during Play Mode. The profiler is paused automatically when the Runtime Atlas window is not visible.

---

## Recorded Metrics

| Metric | Description |
|--------|-------------|
| Frame Time (ms) | Time from start of previous frame to start of current frame |
| FPS | 1000 / frame time |
| GC Heap (MB) | Total allocated GC heap size |
| GC Alloc (KB) | GC allocations in the current frame |
| Draw Calls | Number of draw calls this frame (from `UnityStats`) |
| Triangles | Triangle count (from `UnityStats`) |
| Vertices | Vertex count (from `UnityStats`) |

**Note:** `UnityStats` values reflect the full editor frame, not just game rendering. In Edit Mode all `UnityStats` values are zero.

---

## Graph

The graph plots frame time and FPS over the most recent N samples (N configurable in settings). The X axis is frame index; the Y axis auto-scales.

| Control | Action |
|---------|--------|
| Stat label (legend) | Toggle that line on/off |
| **Pause** / **Resume** | Pause or resume live recording |
| **Clear** | Reset all recorded samples |

---

## Sample List

Below the graph, a scrollable list shows all recorded `PerfSample` values in reverse chronological order (newest first).

| Column | Content |
|--------|---------|
| Frame | `Time.frameCount` |
| Time (ms) | Frame time in milliseconds |
| FPS | Instantaneous FPS |
| GC Heap | GC heap in MB |
| GC Alloc | Per-frame allocation in KB |
| Draw Calls | Draw call count |

---

## Thresholds

Alert thresholds are configurable in **Edit > Project Settings > Runtime Atlas**:

| Threshold | Default |
|-----------|---------|
| Frame time warning (ms) | 33.3 (30 FPS) |
| Frame time critical (ms) | 50.0 (20 FPS) |
| GC alloc warning (KB/frame) | 64 |

When a threshold is exceeded, the affected row in the sample list is tinted accordingly.
