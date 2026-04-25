# Timeline Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Records a circular buffer of per-frame snapshots during Play Mode and provides scrubbing playback after recording stops. Allows post-session review of how runtime values evolved over time.

---

## Recording

The Timeline begins recording automatically when Play Mode starts. It uses a circular buffer — once the buffer is full, the oldest frames are overwritten. Recording stops when Play Mode exits, preserving the buffer for playback.

### Per-Frame Snapshot Fields

| Field | Description |
|-------|-------------|
| **Timestamp** | Editor time in seconds when the frame was sampled |
| **FPS** | Frame rate at this sample |
| **MemoryMB** | GC heap size in MB |
| **ActiveCameras** | Number of active cameras this frame |
| **PlayingAudio** | Number of playing audio sources this frame |
| **AlertCount** | Total non-dismissed alert count this frame |
| **CameraFOV** | FOV of the first active camera (degrees) |
| **MaxAudioVolume** | Volume of the loudest playing source |

---

## Playback Controls

After recording, the Timeline tab shows a scrub bar and playback controls:

| Control | Action |
|---------|--------|
| **◀◀** | Jump to first frame |
| **◀** | Step one frame backward |
| **▶ / ❙❙** | Play / pause automatic playback |
| **▶▶** | Jump to last frame |
| **Scrub bar** | Click or drag to navigate to any recorded frame |

Playback replays the stored snapshot values — it does not re-run game logic.

---

## Buffer Capacity

The default buffer capacity is set in the Timeline settings panel (accessible via the ⚙ icon in the window header). Increasing capacity increases memory usage during recording.

---

## Relationship to the Report

Timeline frame data is included in exported session reports. See [Report Export](../../guides/report-export.md) for format details.
