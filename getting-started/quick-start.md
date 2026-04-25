# Quick Start

**Runtime Atlas v1.1.0**

> Runtime Atlas is a paid product. Purchase it at the
> [Unity Asset Store](https://assetstore.unity.com/packages/slug/367424),
> [itch.io](https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit),
> or [Gumroad](https://toolsstudio.gumroad.com/l/runtime-atlas)
> before following these steps.

---

## Step 1 — Open the Window

```
Window > Runtime Atlas > Open
```

Keyboard shortcut: `Ctrl+Alt+R`

The window is dockable. Dock it alongside the Game view or as a floating window based on preference.

---

## Step 2 — Enter Play Mode

Runtime Atlas reads live scene data during Play Mode. Enter Play Mode in Unity as normal. The window header bar updates to show:

- **LIVE** indicator (green)
- Current FPS
- Active camera count, audio source count, alert count, frame index, GC memory, and play mode state

---

## Step 3 — Review Key Tabs

### Camera
Shows all active cameras, their FOV, clip planes, depth, and culling masks. Edit FOV and clip planes live without leaving the window.

### Audio
Shows all `AudioSource` components and the `AudioListener`. Reports playing state, volume, pitch, and spatial blend per source.

### Alerts
Shows aggregated diagnostic alerts from camera and audio subsystems. Alerts are grouped, severity-filtered, and dismissible.

### Profiler
Records frame time (ms), FPS, GC heap size, GC alloc delta, draw calls, and triangle/vertex counts. The graph updates live.

### Graph
Displays runtime node relationships between cameras, audio sources, and the alert system as a live connection diagram.

---

## Step 4 — Run the Script Scanner

The Script Scanner does not run automatically.

1. Open the **Scanner** tab.
2. Click **Scan Scripts**.
3. Review results. Each result includes the file path, line number, issue description, category, and severity.
4. Open the **Optimizer** tab for actionable fix suggestions derived from scanner results.

---

## Step 5 — Export a Report

1. Open the **Report** tab.
2. Click **Generate Preview** to assemble the current session data.
3. Select an export format: **JSON**, **HTML**, **Markdown**, or **CSV**.
4. Click **Export**.
5. Choose a destination folder. The file is written immediately.

Report data includes: project name, Unity version, platform, session duration, frame statistics, all alerts, and all scanner results.

---

## Step 6 — Optional: Load the Demo Scene

A pre-built demo scene is included:

```
Assets/RuntimeAtlas/Demo/Scene/RA.unity
```

To rebuild it from scratch at any time:

```
Window > Runtime Atlas > Build Demo Scene
```

The demo scene contains cameras, audio sources, physics objects, and a stress tester. It is designed to produce visible data across all Runtime Atlas tabs immediately on Play Mode entry.

---

## Next Steps

- [Window Overview](../reference/window-overview.md) — complete tab and UI reference
- [Keyboard Shortcuts](../reference/keyboard-shortcuts.md) — all menu paths
- [Custom Alert Source](../guides/custom-alert-source.md) — extend the alert system
