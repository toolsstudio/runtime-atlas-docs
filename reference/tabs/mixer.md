# Mixer Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Displays the current values of exposed `AudioMixer` parameters. Works with any mixer configured through the Runtime Atlas auto-config utility or manually.

---

## Requirements

An `AudioMixer` asset with at least one exposed parameter. If none is configured, the tab displays a prompt to run:

```
Window > Runtime Atlas > Auto-Config Audio Mixer
```

See [Audio Mixer Setup](../../guides/audio-mixer-setup.md).

---

## Displayed Data

For each exposed parameter on the configured mixer:

| Field | Description |
|-------|-------------|
| **Parameter name** | Exposed parameter name as set in the AudioMixer asset |
| **Value (dB)** | Current value in decibels |
| **Default** | Default parameter value |

---

## Auto-Config Parameter Names

When configured via the utility, these parameters are exposed:

| Parameter | Group | Default (dB) |
|-----------|-------|-------------|
| `MasterVolume` | Master | 0 |
| `MusicVolume` | Music | 0 |
| `SFXVolume` | SFX | 0 |
| `AmbientVolume` | Ambient | 0 |
| `UIVolume` | UI | 0 |

Custom parameter names are fully supported — the Mixer tab reads all exposed parameters regardless of naming.

---

## Notes

- The Mixer tab is read-only. Adjust parameters through the Unity AudioMixer window or via `AudioMixer.SetFloat()` in game code.
- The **Auto** button re-runs the naming convention auto-apply for the selected mixer.
- The **Rescan** button re-polls the mixer asset list if assets were created or deleted since the window opened.
