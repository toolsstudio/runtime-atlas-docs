# Scene Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Provides a structured overview of the active scene's hierarchy and object statistics. Supplements the Unity Hierarchy window with component counts and object categorisation.

---

## Scene Statistics

| Statistic | Description |
|-----------|-------------|
| **Total GameObjects** | All GameObjects in the loaded scene |
| **Active** | Enabled GameObjects |
| **Inactive** | Disabled GameObjects |
| **With Renderer** | Objects with a `Renderer` component |
| **With Collider** | Objects with a `Collider` component |
| **With Rigidbody** | Objects with a `Rigidbody` component |
| **With AudioSource** | Objects with an `AudioSource` component |
| **With Camera** | Objects with a `Camera` component |
| **With Animator** | Objects with an `Animator` component |

---

## Hierarchy List

Top-level GameObjects and their immediate children. Each entry:

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Active state** | Active / Inactive badge |
| **Component count** | Number of attached components |
| **Ping** | Highlights object in the Hierarchy window |

---

## Refresh Behaviour

Data is populated on tab activation. In large scenes (thousands of objects), the first population may take a frame. The count does not update continuously — click the tab or press **Refresh** to re-poll.
