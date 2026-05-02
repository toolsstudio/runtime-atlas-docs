# Audio Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Monitors all `AudioSource` components and the `AudioListener` in the scene. Reports playback state, volume levels, and spatial configuration. Raises alerts for common audio setup issues.

Available in Play Mode only. Data updates every editor frame.

---

## Listener Section

| Field | Description |
|-------|-------------|
| **Listener** | GameObject name hosting the `AudioListener` |
| **Volume** | `AudioListener.volume` — global volume scale (0–1) |
| **Pause** | `AudioListener.pause` state |

If no `AudioListener` is present, a Warning alert is raised. If more than one is present, a second Warning is raised.

---

## Sources Section

Each `AudioSource` renders as a row.

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Clip** | Assigned `AudioClip` name (`—` if none assigned) |
| **Playing** | Whether the source is actively playing |
| **Volume** | Source volume (0–1) |
| **Pitch** | Pitch multiplier |
| **Loop** | Loop enabled state |
| **Spatial Blend** | 0 = fully 2D, 1 = fully 3D |
| **Priority** | Output priority (0 = highest) |
| **Mute** | Mute state |

---

## Alerts Generated

| Condition | Severity |
|-----------|----------|
| No `AudioListener` in scene | Warning |
| More than one `AudioListener` in scene | Warning |
| Source playing with volume = 0 | Info |

---

## Audio Mixer

The Audio tab covers `AudioSource` components only. For `AudioMixer` parameter inspection, see the [Mixer tab](mixer.md) and [Audio Mixer Setup](../../guides/audio-mixer-setup.md).
