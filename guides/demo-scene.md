# Demo Scene
**Runtime Atlas v1.2.0**

---

## Overview

Runtime Atlas includes a pre-built demo scene designed to produce visible data across all diagnostic tabs immediately on Play Mode entry. The demo scene is not required for normal use — it is a verification and exploration aid.

---

## Scene Location

```
Assets/RuntimeAtlas/Demo/Scene/RA.unity
```

---

## Opening the Demo Scene

1. In the Project window, navigate to `Assets/RuntimeAtlas/Demo/Scene/`.
2. Double-click `RA.unity` to open it.
3. Enter Play Mode.

All Runtime Atlas tabs should immediately show data: cameras, audio sources, rigidbody objects, performance metrics, and alerts.

---

## Rebuilding the Demo Scene

If the demo scene is damaged or missing:

```
Window > Runtime Atlas > Build Demo Scene
```

This executes `RADemoSceneBuilder.BuildDemoScene()`, which:

1. Creates a new Unity scene.
2. Adds cameras, lights, audio sources, rigidbodies, and demo behaviour components.
3. Saves the scene to `Assets/RuntimeAtlas/Demo/Scene/RA.unity`.

The rebuild overwrites any existing scene at that path.

---

## Demo Behaviours

The demo scene uses runtime MonoBehaviours from `RuntimeAtlas.Core.Demo`:

| Behaviour | Purpose |
|-----------|---------|
| `RADemoKinematicMover` | Moves a rigidbody kinematically in a pattern |
| `RADemoSpinner` | Rotates a GameObject continuously |
| `RADemoBouncer` | Applies periodic force to a rigidbody |
| `RADemoStressTester` | Instantiates objects on a timer to increase scene complexity |
| `RADemoController` | Controls all demo behaviours from a single component |

---

## Input System Compatibility

The demo scene includes `RADemoInputCompat`, which conditionally supports both the legacy Input Manager and the new Input System. No manual configuration is required. A console warning about Input Manager deprecation is issued by Unity itself and does not affect demo functionality.

---

## Audio Assets

The demo scene uses three audio clips from `Assets/RuntimeAtlas/Demo/Others/`:

| File | Purpose |
|------|---------|
| `Ambient_Test.wav` | Background ambient loop |
| `BGM_Test.mp3` | Background music source |
| `SFX_Test.mp3` | One-shot sound effect |

These clips are placeholders for testing the Audio tab. They can be replaced with project-specific audio without affecting demo functionality.
