# Quick Start
**Runtime Atlas v1.2.0**

> Runtime Atlas is a paid product. See [Installation](installation.md) for purchase and import instructions.

---

## Step 1 — Open the Window

```
Window > Runtime Atlas > Open
```

Shortcut: `Ctrl+Alt+R`

The window is dockable. Dock it alongside the Game view or float it on a second monitor.

---

## Step 2 — Enter Play Mode

Runtime Atlas reads live scene data during Play Mode. Enter Play Mode normally. The header updates to show:

- **LIVE** indicator (green)
- Current FPS
- Aggregate counts: cameras, audio sources, alerts, frame index, GC memory, play mode state

---

## Step 3 — Review Key Tabs

### Camera
Shows all active cameras. Displays FOV, clip planes, depth, culling mask, and render texture state. FOV and clip planes are editable live.

### Audio
Shows all `AudioSource` components and the `AudioListener` status. Reports playing state, volume, pitch, spatial blend, and a live level meter per source.

### Alerts
Aggregated diagnostic alerts from camera and audio subsystems. Grouped by message, filterable by severity (Info / Warning / Critical), dismissible per alert or all at once.

### Profiler
Records frame time (ms), FPS, GC heap size, GC alloc delta, draw calls, and triangle/vertex counts. Graph updates live and scrolls to follow the current frame.

### Physics
Lists all `Rigidbody` components with velocity, speed, mass, collision detection mode, and physics layer. Includes a full physics layer collision matrix.

### Graph
Displays runtime node relationships between cameras, audio sources, and the alert system as a live interactive diagram.

---

## Step 4 — Scan Scripts

The Script Scanner does not run automatically — it is triggered manually.

1. Open the **Scanner** tab.
2. Click **Scan Scripts**.
3. Review results: each result shows file path, line number, issue description, category, and severity.
4. Open the **Optimizer** tab for fix suggestions derived from scan results.

The scanner is a static pattern analyser. It does not require Play Mode.

---

## Step 5 — Export a Report

1. Open the **Report** tab.
2. Click **Generate Preview**.
3. Select a format: **JSON**, **HTML**, **Markdown**, **CSV**, or **DOCX**.
4. Click **Export** and choose a destination folder.

Report data includes project name, Unity version, platform, session duration, frame statistics, all alerts, and all scanner results.

---

## Step 6 — Optional: Load the Demo Scene

```
Assets/RuntimeAtlas/Demo/Scene/RA.unity
```

To rebuild it:

```
Window > Runtime Atlas > Build Demo Scene
```

The demo scene contains cameras, audio sources, physics objects, animators, and a stress tester — it produces visible data across all tabs immediately on Play Mode entry.

---

## Next Steps

- [Window Overview](../reference/window-overview.md) — complete layout and tab reference
- [Keyboard Shortcuts](../reference/keyboard-shortcuts.md) — all menu paths and shortcuts
- [Custom Alert Source](../guides/custom-alert-source.md) — extend the alert system
- [Report Export](../guides/report-export.md) — export format field reference
