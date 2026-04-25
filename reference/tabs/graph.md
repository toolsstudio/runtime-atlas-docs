# Graph Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Displays a live node-link diagram showing the runtime relationships between cameras, audio sources, the alert system, and the profiler during Play Mode.

---

## Layout

Nodes are arranged automatically based on system type:

| Node type | Represents |
|-----------|-----------|
| **Camera node** | Each active `Camera` component |
| **Audio node** | Each active `AudioSource` and the `AudioListener` |
| **Alert node** | The alert system and its current alert count |
| **Profiler node** | Current frame time and FPS summary |

Edges between nodes indicate data flow — for example, a camera node connected to the alert system node indicates that camera is generating active alerts.

---

## Interaction

- The graph is read-only during Play Mode.
- Clicking a node focuses the corresponding tab (clicking a Camera node navigates to the Camera tab).
- The graph redraws on each editor repaint cycle.

---

## Notes

The graph is a diagnostic aid, not a scene graph or full dependency map. It reflects the subset of scene systems that Runtime Atlas actively monitors.
