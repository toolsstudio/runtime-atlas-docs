# Timeline Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Records a circular buffer of frame snapshots and allows scrubbing through them to review past state. Useful for reviewing what happened immediately before a problem was observed.

---

## Recording

The timeline records automatically during Play Mode. The buffer size is configurable in settings (default: 300 frames). When the buffer is full, oldest frames are overwritten (FIFO).

Each recorded `FrameData` contains:

| Field | Description |
|-------|-------------|
| Frame index | `Time.frameCount` at capture time |
| Frame time (ms) | Frame duration |
| FPS | Instantaneous FPS |
| GC Heap (MB) | GC heap at capture |
| Camera count | Active camera count at capture |
| Source count | Active audio source count at capture |
| Alert count | Active alert count at capture |

---

## Playback Controls

| Control | Action |
|---------|--------|
| Scrubber | Drag to seek to any recorded frame |
| **◀** | Step back one frame |
| **▶** | Step forward one frame |
| **▶▐▐** | Play/pause continuous playback |

Playback replays the recorded data in the display — it does not rewind the Unity scene.

---

## Mini-Graph

Above the scrubber, a mini-graph shows the frame time profile across the full buffer. Peaks indicate frames that took longer than usual. Hover over a peak to see the exact frame index and time value.

---

## Limitations

The timeline buffer is cleared on Play Mode exit. It is not persisted across sessions. Maximum buffer size is bounded by memory; reduce the configured frame count for projects with large scenes.
