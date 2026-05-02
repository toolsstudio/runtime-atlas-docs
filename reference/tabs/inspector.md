# Inspector Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Displays the components of the currently selected `GameObject` in the Unity scene. Functions as a supplementary inspector that remains visible alongside the main Unity Inspector.

---

## Component Display

For each component on the selected GameObject:

| Information | Displayed |
|-------------|----------|
| Component type name | Yes |
| Enabled state | Yes (toggle where applicable) |
| Serialized properties | Yes — via `SerializedObject` / `SerializedProperty` |
| Script reference | Yes — Ping button |

---

## History

The Inspector tab maintains a history of recently inspected GameObjects. Use the back (◀) and forward (▶) arrows to navigate the history.

---

## Pin

Clicking **Pin** locks the inspector to the currently selected object. While pinned, Unity selection changes do not update the displayed object.

---

## Add Component

The **Add Component** button opens the Unity component search dialog. In Unity 6, this uses a Unity 6-compatible path (not `ExecuteMenuItem("Component/Scripts")`).

---

## Limitations

The Runtime Atlas Inspector tab is not a replacement for the Unity Inspector. Complex custom property drawers and inspector overrides that rely on Unity's editor internals may not render correctly. For full inspector functionality, use the Unity Inspector window.
