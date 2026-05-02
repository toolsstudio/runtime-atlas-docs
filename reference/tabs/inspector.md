# Inspector Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Provides a Runtime Atlas-scoped component inspector for the currently selected GameObject. Complements the Unity Inspector with selection history, component pinning, and filtering.

---

## Target Selection

The tab tracks the Unity Editor selection. Select any GameObject in the Hierarchy or Scene view — the tab updates immediately. The current target name and full hierarchy path are shown at the top of the tab.

---

## Component Display

Each component on the selected GameObject renders as a card with:

| Field | Description |
|-------|-------------|
| **Component name** | Type name |
| **Enabled toggle** | Toggle enabled state (where applicable) |
| **Property list** | Serialized properties rendered via Unity's serialization system |

---

## Pinning

- Click **Pin** on any component card to pin it.
- Pinned components remain visible at the top of the list regardless of selection changes.
- Click **Unpin** to release.

Filter buttons:

| Button | Shows |
|--------|-------|
| **Pinned** | Only pinned components |
| **Disabled** | Only disabled components |
| (none) | All components on the current target |

---

## Navigation

| Button | Action |
|--------|--------|
| **Back** | Navigate to the previously inspected object |
| **Next** | Navigate forward in inspection history |
| **Ping** | Highlight the target in the Hierarchy window |
| **Copy Path** | Copy the full hierarchy path to clipboard |
| **Expand All** | Expand all component cards |
| **Collapse All** | Collapse all component cards |

---

## Add Component

The **+ Add Component** button focuses the Unity Inspector window, where the native Add Component workflow is available. This is the correct cross-version approach for Unity 2021.3 through Unity 6 (the `Component/Scripts` menu path used in earlier implementations was removed in Unity 6).

---

## Lock Mode

The **Lock** button prevents the tab from tracking selection changes. The locked target remains displayed until unlocked or until Play Mode exits.
