# Alerts Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Displays all diagnostic alerts raised by Runtime Atlas subsystems during the current session. Alerts are aggregated by group key, so a repeated condition appears as one entry with an occurrence count rather than flooding the list.

---

## Severity Levels

| Level | Meaning |
|-------|---------|
| **Info** | Informational condition. No user action required. |
| **Warning** | Condition that may cause unexpected behaviour. |
| **Critical** | Condition expected to cause a problem. |

---

## Alert Entry Fields

| Field | Description |
|-------|-------------|
| Severity badge | Colour-coded: blue (Info), yellow (Warning), red (Critical) |
| **Message** | Human-readable description of the condition |
| **Source** | Name of the subsystem or object that generated the alert |
| **Time** | Timestamp of the most recent occurrence |
| **Count** | Number of times this alert has been aggregated under its group key |
| **Dismiss** | Removes the entry from the active list for this session |

---

## Filter Toolbar

| Filter | Shows |
|--------|-------|
| **Info** | Info-severity entries only |
| **Warning** | Warning-severity entries only |
| **Critical** | Critical-severity entries only |
| (all active) | All non-dismissed entries |
| **Show Dismissed** | Toggle to include dismissed entries |

---

## Alert Sources

Alerts are contributed by any class implementing `IAlertSource`. Built-in sources:

| Source | Conditions monitored |
|--------|---------------------|
| `CameraInspectorNode` | Clip ratio, depth conflicts, empty culling mask |
| `AudioInspectorNode` | Missing listener, multiple listeners, silent playing source |
| `PerformanceProfiler` | Consecutive slow frames, GC spikes |

Custom sources: see [Custom Alert Source](../../guides/custom-alert-source.md).

---

## Stats Bar Relationship

The **Alerts** field in the stats bar is the current `AlertSystem.Count` — non-dismissed alerts across all severity levels. It updates every editor frame regardless of which tab is active.

---

## Report Export

All alerts — including dismissed — are exported in session reports. Dismissed status is not persisted across sessions; all alerts are treated as active in report data. See [Report Export](../../guides/report-export.md).

---

## Session Lifetime

The alert list is cleared when Play Mode starts (`AlertSystem.Clear()` is called on `EnteredPlayMode`). Alerts from a previous Play Mode session are not available after re-entering Play Mode.
