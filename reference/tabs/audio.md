# Audio Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Monitors all `AudioSource` components and the `AudioListener` in the scene. Reports playback state, volume levels, and spatial audio configuration during Play Mode.

---

## Data Displayed

### Listener Section

| Field | Description |
|-------|-------------|
| **Listener** | Name of the GameObject hosting the `AudioListener` |
| **Volume** | `AudioListener.volume` (global volume scale) |
| **Pause** | Whether `AudioListener.pause` is active |

If no `AudioListener` is present, a Warning alert is raised.

### Sources Section

Each `AudioSource` is displayed as a row showing:

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Clip** | Name of the assigned `AudioClip` (or `—` if none) |
| **Playing** | Whether the source is currently playing |
| **Volume** | Source volume (0–1) |
| **Pitch** | Source pitch multiplier |
| **Loop** | Loop enabled state |
| **Spatial Blend** | 0 = fully 2D, 1 = fully 3D |
| **Priority** | Source priority (0 = highest) |
| **Mute** | Mute state |

---

## BGM / Ambient / SFX Detection

Runtime Atlas identifies sources by name convention in the demo scene:

| Pattern | Category |
|---------|----------|
| Contains `BGM` | Background music |
| Contains `Ambient` | Ambient sound |
| Contains `SFX` | Sound effects |

The stats bar shows the count of detected sources regardless of naming convention.

---

## Audio Mixer

If an `AudioMixer` asset is configured in the project, the **Mixer** tab provides parameter inspection. The Audio tab itself only covers live `AudioSource` components.

For mixer setup, see [Audio Mixer Setup](../../guides/audio-mixer-setup.md).

---

## Alerts Generated

| Condition | Severity | Description |
|-----------|----------|-------------|
| No `AudioListener` in scene | Warning | No audio output path exists |
| Multiple `AudioListener` components | Warning | Unity ignores all but one; behaviour is undefined |
| Source with Volume = 0 and playing | Info | Source is playing silently |
