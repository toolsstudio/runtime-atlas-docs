# Camera Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Displays all `Camera` components in the current scene. In Play Mode, data is sourced from live snapshots polled at up to 60 Hz. In Edit Mode, the camera list is refreshed at most once per second.

---

## Edit Mode Behaviour

In Edit Mode, the tab lists all `Camera` components found in the current scene. The list is read-only — properties cannot be edited in Edit Mode. Post-processing volume data requires a scene with URP or HDRP volumes; without those packages installed, the Advanced sub-tab shows a package requirement notice.

---

## Play Mode Behaviour

In Play Mode, the tab shows live snapshot data. Each camera card updates every frame. FOV, near clip, and far clip can be edited live. Changes made in the camera card write back to the live `Camera` component immediately.

---

## Camera Card

Each camera is shown in a collapsible card.

**Header row:**
- Camera name
- Camera depth
- **Enabled** toggle
- **Sub-tab selector:** Basic / Advanced / Diagnostics

### Basic Sub-tab

| Field | Description |
|-------|-------------|
| Render Path | Forward / Deferred |
| Clear Flags | SkyBox / Solid Color / Depth / Nothing |
| Background | Background clear color |
| Culling Mask | Bitmask of rendered layers |
| Depth | Camera draw order |
| FOV | Field of view in degrees (editable) |
| Near Clip | Near clipping plane (editable) |
| Far Clip | Far clipping plane (editable) |
| Rect | Viewport rect (X, Y, W, H) |
| Render Texture | Target render texture, if assigned |
| Allow HDR | HDR rendering toggle |
| Allow MSAA | MSAA toggle |
| Allow Dynamic Resolution | Dynamic resolution toggle |

### Advanced Sub-tab

Shows post-processing volumes in the scene (requires URP or HDRP). For each volume:

| Field | Description |
|-------|-------------|
| Enabled | Whether the volume is active |
| Scope | Global or Local |
| Name | Volume GameObject name |
| Weight | Blend weight slider (0–1, editable) |

### Diagnostics Sub-tab

| Check | Condition flagged |
|-------|------------------|
| Multiple cameras at same depth | Two or more cameras share the same depth value |
| Camera disabled but exists | `Camera` component is disabled — may be intentional but worth noting |
| No render texture assigned | Applicable when the camera is expected to render to a texture |

---

## Alert Integration

The Camera node generates alerts for the following conditions:

| Alert | Severity |
|-------|---------|
| Multiple cameras rendering to the same depth | Warning |
| Camera with no culling mask layers | Warning |

Alerts appear in the **Alerts** tab and persist for the session until dismissed.
