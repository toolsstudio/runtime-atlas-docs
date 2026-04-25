# Scene Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Provides a structured overview of the active scene's hierarchy and object counts. Supplements the Unity Hierarchy window with statistics and object categorisation.

---

## Scene Statistics

| Statistic | Description |
|-----------|-------------|
| **Total GameObjects** | Count of all GameObjects in the loaded scene |
| **Active** | Count of active (enabled) GameObjects |
| **Inactive** | Count of inactive (disabled) GameObjects |
| **With Renderer** | Count of objects with a `Renderer` component |
| **With Collider** | Count of objects with a `Collider` component |
| **With Rigidbody** | Count of objects with a `Rigidbody` component |
| **With AudioSource** | Count of objects with an `AudioSource` component |
| **With Camera** | Count of objects with a `Camera` component |
| **With Animator** | Count of objects with an `Animator` component |

---

## Hierarchy List

The tab displays the top-level GameObjects and their immediate children. Each entry shows:

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Active state** | Active / Inactive badge |
| **Component count** | Number of components attached |
| **Ping** button | Highlights object in Unity Hierarchy |

---

## Notes

The Scene tab reads data from `FindObjectsOfTypeAll` calls. In large scenes (thousands of objects), the initial population may take a frame. The count refreshes on tab activation and does not update continuously.
