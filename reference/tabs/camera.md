# Camera Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Displays live state for every `Camera` component active in the current scene. Supports non-destructive property editing during Play Mode without modifying the scene.

Available in both Edit Mode and Play Mode. Data updates every editor frame in Play Mode; on tab activation in Edit Mode.

---

## Layout

Each camera renders as an expandable card. The card header shows the camera's GameObject name and enabled state. Cards are ordered by camera depth (lowest first).

---

## Sub-Tabs

Each camera card contains three sub-tabs.

### Basic

| Field | Editable | Description |
|-------|----------|-------------|
| **FOV** | Yes | Field of view in degrees (perspective cameras only). Slider range 1°–179°. |
| **FOV Presets** | Yes | One-click preset buttons: VR 90°, FPS 75°, Film 60°, Portrait 45°, Tele 30° |
| **Near Clip** | Yes | Near clipping plane distance |
| **Far Clip** | Yes | Far clipping plane distance |
| **Depth** | No | Render depth (draw order) |
| **Clear Flags** | No | Skybox, Solid Color, Depth Only, or Don't Clear |
| **Culling Mask** | No | Layer mask of rendered layers |
| **Target Display** | No | Display output index |

### Advanced

| Field | Editable | Description |
|-------|----------|-------------|
| **Orthographic** | No | Projection mode (perspective vs orthographic) |
| **Orthographic Size** | No | Half-height of the orthographic view volume |
| **HDR** | No | High dynamic range rendering state |
| **MSAA** | No | Anti-aliasing sample count |
| **Occlusion Culling** | No | Occlusion culling enabled state |
| **Rendering Path** | No | Use Graphics Settings / Forward / Deferred |
| **Target Texture** | No | Assigned `RenderTexture` (name, or `None`) |
| **Allow Dynamic Resolution** | No | Dynamic resolution enabled state |

### Diagnostics

| Field | Description |
|-------|-------------|
| **Position** | World-space position (live, read-only) |
| **Rotation** | World-space Euler angles (live, read-only) |
| **ACTIVE** badge | Green — camera was rendered this frame |
| **Clip Ratio Warning** | Shown when Far/Near > 3333:1; indicates depth buffer precision risk |

---

## Alerts Generated

| Condition | Severity |
|-----------|----------|
| Far/Near clip ratio > 3333:1 | Warning |
| Two or more cameras at equal depth | Warning |
| Camera with all culling layers disabled | Info |

Alerts appear in the [Alerts tab](alerts.md) and increment the stats bar counter.

---

## Live Editing Behaviour

Property changes apply immediately. Changes are not written to the scene — they revert when Play Mode exits. To persist a change, edit the scene object directly after exiting Play Mode.

---

## Card Actions

| Button | Action |
|--------|--------|
| **Ping** | Highlights the camera's GameObject in the Hierarchy window |
| **Copy Path** | Copies the full scene hierarchy path to the clipboard |
