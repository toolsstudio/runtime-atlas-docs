# Animator Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Monitors `Animator` components on GameObjects in the scene. Displays active state, current animation state machine layer, and parameter values during Play Mode.

---

## Tracked Data

For each `Animator` found in the scene:

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Controller** | Assigned `RuntimeAnimatorController` asset name |
| **Layer count** | Number of state machine layers |
| **Current state** | Name of the currently playing state on layer 0 |
| **Normalised time** | Playback position within the current state (0–1) |
| **Speed** | Animator speed multiplier |
| **Enabled** | Animator component enabled state |

### Parameters

All `AnimatorControllerParameter` values are displayed:

| Parameter type | Displayed as |
|----------------|-------------|
| `Float` | Numeric value |
| `Int` | Numeric value |
| `Bool` | True / False |
| `Trigger` | Active / Inactive |

---

## Notes

The Animator tab reads parameter values each editor frame. It does not write to parameters. Parameter writes during Play Mode must be performed through game code or the Unity Animator window.
