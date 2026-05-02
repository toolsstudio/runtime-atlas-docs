# Settings Reference

**Runtime Atlas v1.2.0**

---

## Opening Settings

```
Edit > Project Settings > Runtime Atlas
```

Or click the **⚙** icon in the Runtime Atlas window header.

---

## Settings Asset

Settings are stored as a `ScriptableObject` at:

```
Assets/RuntimeAtlas/Editor/Resources/RuntimeAtlasSettings.asset
```

This file is created automatically on first window open. It is a Unity asset and should be committed to version control so all team members share the same configuration.

---

## General

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `RefreshInterval` | `float` | `0.1` | UI repaint frequency in seconds. Data sampling runs at ~60 Hz regardless of this value. Increase to reduce repaint overhead on slow machines. |
| `AutoStartTimeline` | `bool` | `true` | Start the Timeline Recorder automatically when Play Mode begins. |
| `CurvedLines` | `bool` | `true` | Render Graph tab edges as cubic Bezier curves. Set to `false` for straight lines. |

---

## Alert System

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `MaxAlertLogSize` | `int` | `200` | Maximum number of alerts stored in the alert list. Oldest entries are discarded when exceeded. |
| `ShowInfoAlerts` | `bool` | `true` | Whether Info-severity alerts are shown in the Alerts tab by default. |

---

## Timeline

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `TimelineBufferSize` | `int` | `1800` | Circular buffer capacity in frames. At 60 FPS, 1800 frames ≈ 30 seconds. Increasing this raises memory usage during recording. |

---

## Performance Profiler

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `SlowFrameThresholdMS` | `float` | `33.3` | Frame time (ms) above which a frame is flagged `IsSlowFrame`. Set to `16.7` for a 60 FPS target; `8.3` for 120 FPS. |
| `CriticalFrameThresholdMS` | `float` | `50.0` | Frame time (ms) at which a critical slow-frame alert is raised. |
| `GCSpikeThresholdBytes` | `long` | `16384` | GC allocation delta (bytes) per frame that triggers `IsGCSpike`. |
| `GCWarningThresholdBytes` | `long` | `65536` | GC allocation delta (bytes) for a Warning-level alert. |
| `GCCriticalThresholdBytes` | `long` | `262144` | GC allocation delta (bytes) for a Critical-level alert. |
| `SlowFrameAlertCount` | `int` | `5` | Number of consecutive slow frames before a profiler alert fires. |
| `AlertCooldownSeconds` | `double` | `2.0` | Minimum interval in seconds between repeated profiler alerts of the same type. |

---

## Console

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `ConsoleClearOnPlay` | `bool` | `true` | Clear the Console tab ring buffer when Play Mode starts. |

---

## Script Scanner

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `ScannerExcludePaths` | `string[]` | `[]` | Asset-relative path prefixes to exclude from scans. Example: `Assets/ThirdParty`. Paths are prefix-matched. |

---

## Notes

- All threshold values take effect immediately — no domain reload or Play Mode restart required.
- Settings are read once per editor update tick (for UI redraw interval) and once per recording frame (for profiler thresholds).
- The `RuntimeAtlasSettings` asset is read via `Resources.Load` inside the Editor assembly. Do not move it outside the `Resources/` folder.
