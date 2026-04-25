# Inspector Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Provides a Runtime Atlas-scoped component inspector for the currently selected GameObject. Complements the Unity Inspector with pinning, grouping, and filtering capabilities.

---

## Selecting a Target

The Inspector tab tracks the Unity Editor selection. Select any GameObject in the Hierarchy or Scene view — the tab updates to show that object's components.

The current target is shown in the **Target** field at the top of the tab. The field also displays the object's full hierarchy path.

---

## Component Display

Each component on the selected GameObject is displayed as a card showing:

| Field | Description |
|-------|-------------|
| **Component name** | Type name of the component |
| **Enabled toggle** | Toggle component enabled state (where applicable) |
| **Properties** | Serialized property list rendered via Unity's serialization system |

---

## Pinning

Components can be pinned to keep them visible regardless of what is selected:

- Click **Pin** on any component card to pin it.
- Pinned components remain visible at the top of the list when selection changes.
- Click **Unpin** to release.

The **Pinned** filter button shows only pinned components. The **Disabled** filter button shows only disabled components.

---

## Add Component

The **+ Add Component** button at the bottom of the Inspector tab focuses the Unity Inspector window, where the native Add Component workflow is available. This is the correct cross-version approach for Unity 2021.3 through Unity 6.

---

## Navigation

| Button | Action |
|--------|--------|
| **Back** | Navigate to previously viewed object |
| **Next** | Navigate forward in view history |
| **Ping** | Highlight the target GameObject in the Hierarchy |
| **Copy Path** | Copy the full hierarchy path to clipboard |
| **Expand** | Expand all component cards |
| **Collapse** | Collapse all component cards |
