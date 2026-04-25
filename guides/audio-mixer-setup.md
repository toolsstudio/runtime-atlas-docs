# Audio Mixer Setup

**Runtime Atlas v1.1.0**

---

## Overview

Runtime Atlas includes a one-click utility that creates and configures an `AudioMixer` asset with five standard bus groups and exposes their volume parameters. Once configured, the Runtime Atlas Mixer tab can read and display those parameters during Play Mode.

---

## Auto-Config Utility

Run via:

```
Window > Runtime Atlas > Auto-Config Audio Mixer
```

### What It Creates

The utility creates the following if they do not already exist:

**Asset path:** `Assets/RuntimeAtlas/Demo/Audio/RADemoMixer.mixer`

**Groups:**

| Group name | Parent | Purpose |
|-----------|--------|---------|
| Master | (root) | Master output |
| Music | Master | Background music |
| SFX | Master | Sound effects |
| Ambient | Master | Ambient / environmental audio |
| UI | Master | UI feedback sounds |

**Exposed parameters:**

| Parameter name | Target group | Property |
|---------------|-------------|----------|
| `MasterVolume` | Master | Volume |
| `MusicVolume` | Music | Volume |
| `SFXVolume` | SFX | Volume |
| `AmbientVolume` | Ambient | Volume |
| `UIVolume` | UI | Volume |

All parameters are exposed at their default value of `0 dB`.

---

## Manual Setup

If the auto-config utility does not meet your project requirements, configure a custom mixer manually:

1. Create an `AudioMixer` asset via `Assets > Create > Audio Mixer`.
2. In the AudioMixer window, create the bus groups required by your project.
3. Right-click the Volume property of each group you want to monitor and select **Expose '[GroupName] Volume' to script**.
4. Rename the exposed parameter in the **Exposed Parameters** panel to a consistent naming scheme.
5. Assign `AudioSource` components to their respective mixer groups via the **Output** field.

Runtime Atlas displays all exposed parameters regardless of name. No specific naming convention is required for the Mixer tab to function.

---

## Assigning Sources to Groups

After creating the mixer:

1. Select each `AudioSource` in the scene.
2. Set its **Output** field to the target mixer group (e.g., `RADemoMixer/Music`).
3. Enter Play Mode. The Mixer tab will show live parameter values.

---

## Accessing Mixer Parameters at Runtime

To adjust mixer parameters from game code:

```csharp
using UnityEngine;
using UnityEngine.Audio;

public class VolumeController : MonoBehaviour
{
    [SerializeField] private AudioMixer m_Mixer;

    // Value is in decibels. Range: typically -80 to 0.
    public void SetMusicVolume(float linearVolume)
    {
        // Convert linear (0–1) to decibels
        float dB = linearVolume > 0.0001f
            ? 20f * Mathf.Log10(linearVolume)
            : -80f;

        m_Mixer.SetFloat("MusicVolume", dB);
    }
}
```

---

## Notes

- The auto-config utility does not modify any existing `AudioMixer` assets. It only creates a new asset at the specified path.
- If `Assets/RuntimeAtlas/Demo/Audio/RADemoMixer.mixer` already exists, the utility does nothing and logs a message to the Unity Console.
- The created mixer is a standard Unity `AudioMixer` asset. It has no dependency on Runtime Atlas at runtime.
