# Architecture Overview

**Runtime Atlas v1.2.0**

---

## Assembly Structure

Runtime Atlas is divided into four assemblies with strict dependency rules.

```
RuntimeAtlas.Core              (Runtime, ships in player)
  └── RuntimeAtlas.Core.Demo  (Runtime, demo only, ships in player)

RuntimeAtlas.Editor            (Editor only, not in player build)
  ├── depends on: RuntimeAtlas.Core
  └── RuntimeAtlas.Editor.Demo (Editor only)
       └── depends on: RuntimeAtlas.Core.Demo
```

| Assembly | Namespace | Player build | Purpose |
|----------|-----------|-------------|---------|
| `RuntimeAtlas.Core` | `RuntimeAtlas` | Yes | Public data types shipped with player builds |
| `RuntimeAtlas.Core.Demo` | `RuntimeAtlas` | Yes (demo) | Demo scene MonoBehaviours |
| `RuntimeAtlas.Editor` | `RuntimeAtlas.Editor` | No | All editor systems, windows, and modules |
| `RuntimeAtlas.Editor.Demo` | `RuntimeAtlas.Editor` | No | Demo scene builder editor utility |

`RuntimeAtlas.Editor` does **not** reference `RuntimeAtlas.Core.Demo`. The demo-editor dependency is isolated in `RuntimeAtlas.Editor.Demo`.

---

## Public Types in `RuntimeAtlas.Core`

These are the only types that cross the editor/runtime boundary and ship in player builds.

| Type | Kind | Description |
|------|------|-------------|
| `AlertSeverity` | `enum` | Info / Warning / Critical |
| `AlertEntry` | `struct` | One alert record |

All other Runtime Atlas types are editor-only and live in `RuntimeAtlas.Editor`.

---

## Editor Module Map

All editor systems are instantiated by `AtlasWindow.InitModules()` and stored as private fields on the window. There is no service locator or static registry — all modules are owned by the window instance.

```
AtlasWindow
│
├── Data collection (polled in OnEditorUpdate at ~60 Hz)
│     ├── CameraInspectorNode       — Camera polling and snapshot storage
│     ├── AudioInspectorNode        — AudioSource polling and snapshot storage
│     ├── PerformanceProfiler       — Frame time / GC / draw call recording
│     ├── PhysicsInspector          — Rigidbody polling
│     ├── MaterialInspector         — Renderer/material polling
│     ├── AnimatorMonitor           — Animator state and parameter polling
│     ├── AudioMixerPanel           — AudioMixer parameter polling
│     └── AlertSystem               — Alert aggregation (evaluated from node data)
│
├── Recording
│     ├── TimelineRecorder          — Circular buffer of FrameData snapshots
│     └── ConsoleCapture            — Prefixed Unity log intercept, ring buffer
│
├── Tab UI (DrawGUI called by AtlasWindow.DrawActiveTab each repaint)
│     ├── CameraInspectorNode       — Camera tab
│     ├── AudioInspectorNode        — Audio tab
│     ├── GraphLinkVisualizer       — Graph tab (no outer ScrollView)
│     ├── TimelinePlaybackUI        — Timeline tab
│     ├── AlertSystem               — Alerts tab
│     ├── PerformanceProfilerPanel  — Profiler tab
│     ├── PhysicsInspectorPanel     — Physics tab
│     ├── ScriptScanner             — Scanner tab (via DrawScannerTab)
│     ├── OptimizerSuggestions      — Optimizer tab
│     ├── ScriptViewerWindow        — Scripts tab (via DrawScriptsTab)
│     ├── ComponentInspectorPanel   — Inspector tab
│     ├── AnimatorMonitor           — Animator tab
│     ├── AudioMixerPanel           — Mixer tab
│     ├── SceneOverviewPanel        — Scene tab
│     ├── RAReportPanel             — Report tab
│     ├── ConsoleMirrorPanel        — Console tab
│     └── MaterialInspectorPanel    — Materials tab
│
└── Report export
      ├── RAReportGenerator         — Assembles ReportData and writes formats
      └── RAReportPanel             — Report tab UI
```

---

## Data Flow

```
EditorApplication.update (~60 Hz)
    │
    ├─► CameraInspectorNode.Poll()       → Snapshots[]
    ├─► AudioInspectorNode.Poll()        → Snapshots[]
    ├─► PerformanceProfiler.Poll()       → PerfSample circular buffer
    ├─► PhysicsInspector.Poll()          → RigidbodyData[]
    ├─► MaterialInspector.Poll()         → MaterialData[]
    ├─► AnimatorMonitor.Poll()           → AnimatorData[]
    ├─► AudioMixerPanel.Poll()           → MixerParameter[]
    └─► AlertSystem.Evaluate(nodes)      → AlertEntry list
             │
             └─► TimelineRecorder.RecordFrame(nodes, alertSystem)
                                          → FrameData circular buffer

EditorApplication.update (configurable interval, default 0.1s)
    └─► AtlasWindow.Repaint()
              │
              └─► OnGUI()
                    ├─► DrawHeader()
                    ├─► DrawTabBar()
                    ├─► DrawStatsBar()      (reads from all module state)
                    └─► DrawActiveTabSafely()
                              └─► DrawActiveTab()
                                    └─► module.DrawGUI()  (reads cached state, no new polls)
```

Data collection and UI rendering are fully decoupled. Modules collect data in `OnEditorUpdate` at ~60 Hz and store it in cached fields. The tab `DrawGUI` methods read from those cached fields — they do not poll or allocate in the hot GUI path.

---

## Alert System Architecture

```
IAlertSource  (interface)
    │
    ├── CameraInspectorNode   — implements IAlertSource
    ├── AudioInspectorNode    — implements IAlertSource
    └── PerformanceProfiler   — implements IAlertSource
    (custom implementations)

AlertSystem.Evaluate(sources, timestamp)
    │
    └── calls IAlertSource.EvaluateAlerts() on each registered source
         │
         └── source calls AlertSystem.AddAlert(...)
               │
               └── deduplicated by groupKey + minIntervalSeconds
                    → stored in AlertEntry list
```

Custom alert sources can implement `IAlertSource` in an Editor-only script. See [Custom Alert Source](../guides/custom-alert-source.md).

---

## IMGUI Layout Safety

`AtlasWindow.OnGUI` opens a `GUILayout.BeginArea` and, for all tabs except Graph, a `GUILayout.BeginScrollView`. These are closed in a `finally` block, with each `End` call wrapped in its own `try/catch` to prevent secondary exceptions masking the primary error.

`DrawActiveTabSafely` wraps each module's `DrawGUI` in a `BeginVertical`/`EndVertical` buffer layer. If a module throws after opening layout groups, the buffer absorbs the stack damage. `GUIUtility.ExitGUI()` is called to force `IMGUIContainer` to reset `GUILayoutUtility` for the next repaint, guaranteeing a clean layout stack on recovery.

---

## Settings

All configurable values are stored in `RuntimeAtlasSettings` (`ScriptableObject`, loaded via `Resources.Load`). There are no static config fields in module classes. See [Settings Reference](../reference/settings.md).

---

## Version Constant

The canonical version string is `AtlasWindow.k_Version` (`"Version 1.2.0"`). It is also displayed in `RASettingsProvider` as `"Version 1.2.0 | Tools Studio"`. All `.cs` file headers carry the matching asset version line.
