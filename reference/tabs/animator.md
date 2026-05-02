# Animator Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Monitors `Animator` components in the scene. In Play Mode, shows live state machine state, parameter values, and transition info. In Edit Mode, lists all Animators with their controller assignment.

---

## Edit Mode

Lists all `Animator` components in the scene with their GameObject name and assigned `RuntimeAnimatorController`. Click the jump icon to select the GameObject.

The list is refreshed at most once per second.

---

## Play Mode

For each Animator with a valid controller:

**State Info:**

| Field | Description |
|-------|-------------|
| Current State | Name of the current state in the base layer |
| Normalized Time | Playback position within the current state (0–1) |
| Layer count | Number of animation layers |

**Parameters:**

| Parameter type | Display |
|----------------|---------|
| Float | Editable slider |
| Int | Editable integer field |
| Bool | Toggle |
| Trigger | Button (fires the trigger) |

Parameter values can be read and written live from the Animator tab without modifying scene assets.

---

## Search Filter

The search field at the top of the tab filters animators by GameObject name.
