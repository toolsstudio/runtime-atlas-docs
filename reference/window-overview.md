# Window Overview

**Runtime Atlas v1.2.0**

---

## Opening the Window

```
Window > Runtime Atlas > Open    Ctrl+Alt+R
```

The window is a standard dockable `EditorWindow`. It can be docked, floated, or tabbed alongside any other Unity window. Minimum size: 520 × 300 px.

---

## Layout

```
┌──────────────────────────────────────────────────────────────┐
│  Header Bar                                                   │
│  Runtime Atlas    LIVE    168 FPS                        ⚙   │
├──────────────────────────────────────────────────────────────┤
│  Tab Row 1  (7 tabs)                                          │
│  Camera │ Audio │ Graph │ Timeline │ Alerts │ Profiler │ ... │
├──────────────────────────────────────────────────────────────┤
│  Tab Row 2  (11 tabs)                                         │
│  Scanner │ Optimizer │ Scripts │ Inspector │ Animator │ ...  │
├──────────────────────────────────────────────────────────────┤
│  Stats Bar                                                    │
│  Cameras: 3  Sources: 3  Alerts: 6  Frame: 512  GC: 64.2MB  │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  Tab Content Area                                             │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## Header Bar

Always visible regardless of active tab.

| Element | Description |
|---------|-------------|
| **Runtime Atlas** | Window title (static label) |
| **LIVE** / **EDIT MODE** | Green in Play Mode, muted in Edit Mode |
| **FPS** | Current frames per second; appears only in Play Mode when the timeline has a recorded frame |
| **⚙** | Opens the Runtime Atlas settings panel (`Edit > Project Settings > Runtime Atlas`) |

---

## Stats Bar

Updates every editor frame. All counts reflect the moment of the last poll cycle.

| Field | Source | Description |
|-------|--------|-------------|
| **Cameras** | `CameraInspectorNode` | Active `Camera` components in the current scene |
| **Sources** | `AudioInspectorNode` | Active `AudioSource` components in the current scene |
| **Alerts** | `AlertSystem` | Non-dismissed alert count across all severities |
| **Frame** | `TimelineRecorder` | Number of frames recorded in the current buffer |
| **GC Mem** | `System.GC` | Current managed heap size in MB |
| **Mode** | `Application.isPlaying` | `PLAY` during Play Mode; absent in Edit Mode |

Alert count is highlighted in yellow when greater than zero.  
GC Mem is shown in green below 200 MB, yellow up to 500 MB, and red above 500 MB.

---

## Tab Rows

### Row 1 — Runtime Systems

| Index | Tab | Purpose |
|-------|-----|---------|
| 0 | Camera | Live camera diagnostics and property editor |
| 1 | Audio | AudioListener and AudioSource monitoring |
| 2 | Graph | Runtime node relationship diagram |
| 3 | Timeline | Circular frame snapshot recorder and playback |
| 4 | Alerts | Aggregated diagnostic alerts |
| 5 | Profiler | Frame time, FPS, GC, and draw call recording |
| 6 | Physics | Scene rigidbody and physics statistics |

### Row 2 — Tools

| Index | Tab | Purpose |
|-------|-----|---------|
| 7 | Scanner | C# script issue detection |
| 8 | Optimizer | Actionable suggestions from scanner results |
| 9 | Scripts | Script file viewer with line navigation |
| 10 | Inspector | Component inspector for selected GameObject |
| 11 | Animator | Animator parameter and state monitor |
| 12 | Mixer | Audio Mixer parameter viewer |
| 13 | Scene | Scene hierarchy and object statistics |
| 14 | Report | Session report generation and export |
| 15 | Console | Prefixed log capture |
| 16 | Materials | Scene material and shader overview |
| 17 | About | Version and publisher information |

The active tab is highlighted with a red border accent at the top of the button. Tabs are not keyboard-navigable; use the `Window > Runtime Atlas > Tabs` submenu for direct navigation.

---

## Content Area

The content area renders below the stats bar. All tabs except **Graph** render inside a scrollable `GUILayout.BeginScrollView`/`EndScrollView`. The Graph tab renders directly in a `GUILayout.BeginArea` without scroll interception to preserve drag and zoom interactions.

---

## Tab Documentation

Each tab is documented separately in [reference/tabs/](tabs/README.md).
