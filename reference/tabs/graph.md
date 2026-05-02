# Graph Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Displays runtime node relationships between cameras, audio sources, and the alert system as an interactive node graph. The graph updates during Play Mode when the window is visible.

---

## Nodes

| Node type | Represents |
|-----------|-----------|
| Camera | A `Camera` component in the scene |
| Audio Source | An `AudioSource` component |
| Alert System | The `AlertSystem` singleton |

---

## Edges

Edges between nodes represent logical relationships:

- Camera → Alert System: the camera node feeds alerts to the alert system
- Audio Source → Alert System: the audio node feeds alerts to the alert system

---

## Navigation

| Action | Input |
|--------|-------|
| Pan | Middle-mouse drag, or right-mouse drag |
| Zoom | Scroll wheel |
| Select node | Left-click |
| Move node | Left-click and drag |
| Reset layout | **Reset Layout** button |

---

## Limitations

The Graph tab shows the tool's own internal module graph — it does not represent scene graph relationships, prefab hierarchies, or component dependencies. It is a diagnostic view of how Runtime Atlas modules connect to each other.
