# Mixer Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Displays the current values of exposed `AudioMixer` parameters during Play Mode. Works with any `AudioMixer` configured through the Runtime Atlas auto-config utility or manually.

---

## Requirements

The Mixer tab requires an `AudioMixer` asset with exposed parameters. To configure one automatically, use:

```
Window > Runtime Atlas > Auto-Config Audio Mixer
```

See [Audio Mixer Setup](../../guides/audio-mixer-setup.md) for full setup instructions.

---

## Displayed Data

For each exposed parameter on the configured mixer:

| Field | Description |
|-------|-------------|
| **Parameter name** | The exposed parameter name as set in the AudioMixer asset |
| **Value (dB)** | Current value in decibels |
| **Default** | Default value for comparison |

---

## Expected Parameters

When configured via the auto-config utility, Runtime Atlas exposes and monitors the following parameter names:

| Parameter | Default (dB) | Description |
|-----------|-------------|-------------|
| `MasterVolume` | 0 | Master output volume |
| `MusicVolume` | 0 | Background music bus |
| `SFXVolume` | 0 | Sound effects bus |
| `AmbientVolume` | 0 | Ambient sound bus |
| `UIVolume` | 0 | UI sound bus |

Custom parameter names are also supported — the Mixer tab displays all exposed parameters regardless of naming convention.

---

## Notes

- The Mixer tab is read-only. Adjust mixer parameters through the Unity AudioMixer window or via `AudioMixer.SetFloat()` in game code.
- If no mixer is configured, the tab displays a prompt to run the auto-config utility.
