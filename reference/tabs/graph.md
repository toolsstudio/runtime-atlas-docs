# Graph Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Displays a live node-link diagram of runtime relationships between the systems Runtime Atlas monitors. Provides a spatial overview of which systems have active connections or are generating alerts.

---

## Nodes

| Node type | Represents |
|-----------|-----------|
| Camera node | Each active `Camera` component |
| Audio node | Each active `AudioSource` and the `AudioListener` |
| Alert node | The alert system with current non-dismissed alert count |
| Profiler node | Current frame time and FPS summary |

---

## Edges

Edges represent data flow. A camera node connected to the alert system node indicates that camera is the source of one or more active alerts. The alert count on the edge label updates each frame.

Edge style (curved Bezier or straight) is configurable in Project Settings (`CurvedLines`).

---

## Interaction

| Action | Effect |
|--------|--------|
| Click a node | Navigates to the tab corresponding to that system |
| Drag canvas | Pan the graph view |
| Scroll | Zoom in/out |
| Right-click | Context menu (reset view, etc.) |

The Graph tab renders directly in a `BeginArea` without an outer `ScrollView`, preserving drag and zoom behaviour. Scroll input is not intercepted by the window's content scroll.

---

## Notes

- The graph is a diagnostic aid, not a full scene dependency map. It reflects only the systems Runtime Atlas actively monitors.
- Nodes are repositioned on each repaint if the scene camera or audio source count changes.
- The graph is read-only in both Edit Mode and Play Mode. System connections are derived from live data, not user configuration.
