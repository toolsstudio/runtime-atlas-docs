# Audio Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Displays all `AudioSource` components and the `AudioListener` status. In Play Mode, data comes from live snapshots. In Edit Mode, the source list is refreshed at most once per second.

---

## AudioListener Status

The top row of the tab shows the current `AudioListener` status:

| State | Badge |
|-------|-------|
| Exactly one listener found | OK (green) |
| No listener found | NOT FOUND (red) |
| Multiple listeners found | MULTIPLE (n) (yellow) |

Unity requires exactly one active `AudioListener` in the scene for audio to function correctly. Multiple listeners produce undefined mixing behaviour.

---

## AudioSource Cards

Each `AudioSource` is shown in a card.

**Header row:**
- Source name
- Playing state badge (PLAYING / PAUSED / STOPPED)
- Enabled toggle
- Volume slider

### Fields

| Field | Description |
|-------|-------------|
| Clip | Clip name, or "(none)" if no clip assigned |
| Playing | Whether the source is currently playing |
| Volume | 0.0 – 1.0 |
| Pitch | Pitch multiplier |
| Spatial Blend | 0 = fully 2D, 1 = fully 3D |
| Loop | Loop toggle |
| Mute | Mute toggle |
| Min Distance | 3D audio attenuation start distance |
| Max Distance | 3D audio attenuation end distance |
| Level Meter | Approximate current output level (visual bar) |
| Playback Position | Current playback time / clip length (Play Mode only) |

### Playback Controls (Play Mode)

| Button | Action |
|--------|--------|
| ▶ Play | `source.Play()` |
| ▐▐ Pause | `source.Pause()` |
| ■ Stop | `source.Stop()` |

---

## Alert Integration

| Alert | Severity |
|-------|---------|
| No AudioListener in scene | Critical |
| Multiple AudioListeners in scene | Warning |
| AudioSource with no clip assigned | Info |
| AudioSource looping in Play Mode | Info |
