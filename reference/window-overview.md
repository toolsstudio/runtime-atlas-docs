# Window Overview

**Runtime Atlas v1.1.0**

---

## Opening the Window

```
Window > Runtime Atlas > Open    Ctrl+Alt+R
```

The window is a standard dockable Unity `EditorWindow`. It can be docked, floated, or tabbed alongside any other Unity window.

---

## Window Layout

```
┌─────────────────────────────────────────────────────┐
│  Header Bar                                          │
│  Runtime Atlas   LIVE   168 FPS   ⚙                │
├─────────────────────────────────────────────────────┤
│  Tab Row 1                                           │
│  Camera │ Audio │ Graph │ Timeline │ Alerts │ ...   │
├─────────────────────────────────────────────────────┤
│  Tab Row 2                                           │
│  Scanner │ Optimizer │ Scripts │ Inspector │ ...    │
├─────────────────────────────────────────────────────┤
│  Stats Bar                                           │
│  Cameras: 3  Sources: 3  Alerts: 6  Frame: 300 ...  │
├─────────────────────────────────────────────────────┤
│                                                      │
│  Tab Content Area                                    │
│                                                      │
└─────────────────────────────────────────────────────┘
```

---

## Header Bar

The header bar is always visible regardless of which tab is active.

| Element | Description |
|---------|-------------|
| **Runtime Atlas** | Window title |
| **LIVE** | Green indicator — window is connected and updating |
| **FPS** | Current frames per second (updates every frame in Play Mode) |
| **⚙ (Settings)** | Opens the Runtime Atlas settings panel |

---

## Stats Bar

The stats bar shows aggregate counts updated each frame:

| Field | Description |
|-------|-------------|
| **Cameras** | Number of active `Camera` components found in the scene |
| **Sources** | Number of active `AudioSource` components |
| **Alerts** | Number of non-dismissed alerts currently active |
| **Frame** | Current `Time.frameCount` |
| **GC Mem** | Current GC heap size in MB |
| **Mode** | `PLAY` during Play Mode, `EDIT` in Edit Mode |

---

## Tab Layout

Tabs are split across two rows.

**Row 1 — Runtime Systems**

| Index | Tab | Purpose |
|-------|-----|---------|
| 0 | Camera | Live camera diagnostics and property editor |
| 1 | Audio | Audio listener and source monitoring |
| 2 | Graph | Runtime node relationship diagram |
| 3 | Timeline | Circular frame snapshot playback |
| 4 | Alerts | Aggregated diagnostic alerts |
| 5 | Profiler | Frame time, FPS, GC, and draw call recording |
| 6 | Physics | Scene rigidbody and physics statistics |

**Row 2 — Tools**

| Index | Tab | Purpose |
|-------|-----|---------|
| 7 | Scanner | C# script issue detection |
| 8 | Optimizer | Suggestions derived from scanner results |
| 9 | Scripts | Script file viewer with line navigation |
| 10 | Inspector | Component inspector for selected GameObject |
| 11 | Animator | Animator parameter and state monitor |
| 12 | Mixer | Audio Mixer parameter viewer |
| 13 | Scene | Scene hierarchy and object overview |
| 14 | Report | Session report generation and export |
| 15 | Console | Prefixed log capture (`[RA]` tagged messages) |
| 16 | Materials | Scene material and shader overview |
| 17 | About | Package version, publisher information |

---

## Individual Tab Documentation

Each tab is documented separately:

- [Camera](tabs/camera.md)
- [Audio](tabs/audio.md)
- [Graph](tabs/graph.md)
- [Timeline](tabs/timeline.md)
- [Alerts](tabs/alerts.md)
- [Profiler](tabs/profiler.md)
- [Physics](tabs/physics.md)
- [Scanner](tabs/scanner.md)
- [Optimizer](tabs/optimizer.md)
- [Scripts](tabs/scripts.md)
- [Inspector](tabs/inspector.md)
- [Animator](tabs/animator.md)
- [Mixer](tabs/mixer.md)
- [Scene](tabs/scene.md)
- [Report](tabs/report.md)
- [Console](tabs/console.md)
- [Materials](tabs/materials.md)
