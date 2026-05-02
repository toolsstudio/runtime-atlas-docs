# Timeline Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Records a fixed-capacity circular buffer of per-frame cross-system snapshots during Play Mode. Provides scrub playback after recording stops for post-session review.

---

## Recording

Recording starts automatically when Play Mode begins if `AutoStartTimeline` is enabled in Project Settings (default: enabled). The buffer is circular — when full, new frames overwrite the oldest. Recording stops when Play Mode exits, preserving the buffer for playback.

---

## Per-Frame Snapshot Fields

| Field | Type | Description |
|-------|------|-------------|
| `Timestamp` | `double` | Editor time (seconds) when the frame was sampled |
| `FPS` | `float` | Frames per second at this sample |
| `MemoryMB` | `float` | GC heap size in MB |
| `ActiveCameras` | `int` | Active `Camera` components this frame |
| `PlayingAudio` | `int` | Actively playing `AudioSource` components this frame |
| `AlertCount` | `int` | Total non-dismissed alert count this frame |
| `CameraFOV` | `float` | FOV of the first active camera (degrees) |
| `MaxAudioVolume` | `float` | Volume of the loudest actively playing source |

---

## Playback Controls

| Control | Action |
|---------|--------|
| **◀◀** | Jump to first recorded frame |
| **◀** | Step one frame backward |
| **▶ / ❙❙** | Play / pause automatic playback |
| **▶▶** | Jump to last recorded frame |
| **Scrub bar** | Click or drag to navigate to any frame |

Playback replays stored snapshot values. It does not re-run game logic.

---

## Buffer Capacity

Default: 1800 frames (≈ 30 seconds at 60 FPS). Configurable via `TimelineBufferSize` in Project Settings. Increasing capacity raises memory usage proportionally.

---

## Stats Bar

The **Frame** field in the stats bar shows the current `TimelineRecorder.FrameCount` — the number of valid frames in the buffer, not the Unity `Time.frameCount`.

---

## Relationship to Profiler

Timeline and Profiler are independent recorders. The Report tab uses profiler frame data (`PerfSample` records). Timeline snapshots are not included in exported reports.
