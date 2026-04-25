# Camera Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Displays live state for every `Camera` component active in the current scene. Allows non-destructive property editing during Play Mode without modifying the scene.

---

## Data Displayed

Each camera is shown as an expandable card. The card header shows the camera's GameObject name and enabled state.

### Basic Sub-Tab

| Field | Description |
|-------|-------------|
| **FOV** | Field of view in degrees. Editable via slider. |
| **Presets** | One-click FOV presets: VR 90°, FPS 75°, Film 60°, Portrait 45°, Tele 30° |
| **Near Clip** | Near clipping plane distance |
| **Far Clip** | Far clipping plane distance |
| **Depth** | Render depth (draw order) |
| **Clear Flags** | Skybox, Solid Color, Depth Only, or Don't Clear |
| **Culling Mask** | Rendered layer mask |
| **Target Display** | Display output index |

### Advanced Sub-Tab

| Field | Description |
|-------|-------------|
| **Orthographic** | Toggle between perspective and orthographic projection |
| **Orthographic Size** | Half-height of the orthographic view |
| **HDR** | High dynamic range rendering |
| **MSAA** | Multi-sample anti-aliasing level |
| **Occlusion Culling** | Occlusion culling enabled state |
| **Rendering Path** | Use Graphics Settings / Forward / Deferred |
| **Target Texture** | Assigned `RenderTexture` (if any) |
| **Allow Dynamic Resolution** | Dynamic resolution enabled state |

### Diagnostics Sub-Tab

| Field | Description |
|-------|-------------|
| **Position** | World-space position (read-only, live) |
| **Rotation** | World-space Euler angles (read-only, live) |
| **Clip Ratio Warning** | Shown when `Far / Near > 3333:1` — indicates potential depth precision loss |
| **ACTIVE indicator** | Green badge — camera rendered this frame |

---

## Alerts Generated

The Camera tab contributes the following alerts to the Alert system:

| Condition | Severity | Description |
|-----------|----------|-------------|
| Far/Near clip ratio > 3333:1 | Warning | High clip ratio degrades depth buffer precision |
| Multiple cameras with equal depth | Warning | Cameras at the same depth render in undefined order |
| Camera with no culling layers | Info | Camera renders nothing |

Alerts are visible in the **Alerts** tab and the stats bar count.

---

## Live Editing

Property changes made in the Camera tab take effect immediately during Play Mode. Changes are not persisted to the scene — they revert when Play Mode exits. To persist changes, apply them directly to the scene object in the Inspector after exiting Play Mode.

---

## Ping and Navigation

Each camera card includes **Ping** and **Copy Path** buttons:

- **Ping** — highlights the camera's GameObject in the Hierarchy window.
- **Copy Path** — copies the full scene hierarchy path to the clipboard.
