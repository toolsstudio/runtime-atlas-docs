# Animator Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Monitors `Animator` components active in the scene. Displays current state, layer info, and parameter values during Play Mode.

---

## Tracked Data

For each `Animator` found:

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Controller** | Assigned `RuntimeAnimatorController` asset name |
| **Layer count** | Number of state machine layers |
| **Current state** | Name of the playing state on layer 0 |
| **Normalised time** | Playback position within the current state (0–1) |
| **Speed** | Animator speed multiplier |
| **Enabled** | Component enabled state |

---

## Parameters

All `AnimatorControllerParameter` values are displayed per Animator:

| Parameter type | Display |
|----------------|---------|
| `Float` | Numeric value |
| `Int` | Numeric value |
| `Bool` | `True` / `False` |
| `Trigger` | `Active` / `Inactive` |

---

## Refresh

The Animator list is populated by polling the scene on tab activation and on each **Refresh** button press. It does not update continuously in Edit Mode. In Play Mode, parameter values update every editor frame; the Animator list itself updates on each poll cycle.

---

## Notes

- The Animator tab is read-only. Parameters cannot be set from this tab.
- Parameter values update each editor frame during Play Mode. There is no write path.
- Writes must go through `Animator.SetFloat`, `SetBool`, etc. in game code or via the Unity Animator window.
