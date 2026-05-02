# Scene Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Displays a summary of all GameObjects in the current scene with counts by component type. Provides a search field to filter by name.

---

## Summary Row

At the top of the tab, aggregate counts:

| Count | Description |
|-------|-------------|
| Total objects | All GameObjects in the scene |
| Active | GameObjects with `activeInHierarchy == true` |
| Inactive | GameObjects with `activeInHierarchy == false` |
| With scripts | GameObjects with at least one MonoBehaviour |

---

## Object List

Each row in the list represents one GameObject:

| Column | Description |
|--------|-------------|
| Name | GameObject name |
| Active | Active state indicator |
| Layer | Layer name |
| Components | Component count |
| Tag | GameObject tag |

Clicking a row selects the GameObject in the Unity Editor (updates the Selection and highlights it in the scene view).

---

## Search

The search field filters the list by GameObject name (case-insensitive substring match). The filter applies immediately on each keystroke.

---

## Limitations

For large scenes (1,000+ objects) the object list rebuild can be slow. Using the search filter to narrow the list improves performance.
