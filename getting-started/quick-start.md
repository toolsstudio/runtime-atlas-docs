# Quick Start

**Runtime Atlas v1.2.0**

> Runtime Atlas is a paid product. Purchase at the [Unity Asset Store](https://assetstore.unity.com/packages/slug/367424), [itch.io](https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit), or [Gumroad](https://toolsstudio.gumroad.com/l/runtime-atlas) before following these steps.

---

## Step 1 — Open the Window

```
Window > Runtime Atlas > Open    Ctrl+Alt+R
```

The window is a standard dockable `EditorWindow`. Dock it alongside the Game view or float it.

---

## Step 2 — Enter Play Mode

Enter Play Mode normally. The window header updates:

- Status changes from **EDIT MODE** to **LIVE**
- Current FPS appears next to the status indicator
- Stats bar updates: camera count, audio source count, alert count, frame index, GC memory

---

## Step 3 — Review the Core Tabs

### Camera

Live state for every active `Camera` in the scene — FOV, clip planes, depth, culling mask. Edit FOV and clip planes directly without leaving the window. Changes revert on Play Mode exit.

### Audio

All `AudioSource` components and the `AudioListener`. Playing state, volume, pitch, spatial blend, and loop per source.

### Alerts

Aggregated diagnostic alerts from camera, audio, and profiler subsystems. Each entry shows severity, message, source, timestamp, and occurrence count. Filter by severity or dismiss individually.

### Profiler

Frame time (ms), FPS, GC heap size, GC alloc delta, draw calls, triangles, and vertices. Graph updates live. Slow frames highlighted. GC spikes marked.

### Graph

Node diagram showing runtime relationships between cameras, audio sources, the alert system, and the profiler. Read-only; click a node to navigate to its tab.

---

## Step 4 — Scan Scripts

The Scanner does not run automatically.

1. Open the **Scanner** tab.
2. Click **Scan Scripts**.
3. Results list file path, line number, issue description, category, and severity.
4. Click any result row to open that file at the flagged line in the **Scripts** tab.
5. Open the **Optimizer** tab for structured fix suggestions derived from scan results.

---

## Step 5 — Export a Report

1. Open the **Report** tab.
2. Click **Generate Preview** to assemble current session data.
3. Select a format: **JSON**, **HTML**, **Markdown**, **CSV**, or **DOCX**.
4. Click **Export** and choose a destination folder.

Report data: project name, Unity version, platform, session duration, frame statistics, all alerts, and all scanner results.

---

## Step 6 — Optional: Run the Demo Scene

```
Assets/RuntimeAtlas/Demo/Scene/RA.unity
```

Open, enter Play Mode, and open Runtime Atlas. All tabs populate with real data immediately. See [Demo Scene](../guides/demo-scene.md).

To rebuild the demo scene from scratch:

```
Window > Runtime Atlas > Build Demo Scene
```

---

## Next Steps

| Document | Purpose |
|----------|---------|
| [Window Overview](../reference/window-overview.md) | Complete UI anatomy |
| [Settings Reference](../reference/settings.md) | Configure thresholds and buffer sizes |
| [Custom Alert Source](../guides/custom-alert-source.md) | Extend the alert system |
| [Report Export](../guides/report-export.md) | Format reference and field mapping |
