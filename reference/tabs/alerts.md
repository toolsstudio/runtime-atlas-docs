# Alerts Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Displays all diagnostic alerts raised by Runtime Atlas subsystems during the current session. Alerts are aggregated by group key so repeated conditions appear as a single entry with an occurrence count.

---

## Alert Severity Levels

| Level | Value | Meaning |
|-------|-------|---------|
| `Info` | 0 | Informational condition. No action required. |
| `Warning` | 1 | Condition that may cause unexpected behaviour. |
| `Critical` | 2 | Condition that will likely cause a problem. |

---

## Alert List

Each alert entry shows:

| Field | Description |
|-------|-------------|
| **Severity badge** | Colour-coded: blue (Info), yellow (Warning), red (Critical) |
| **Message** | Human-readable description of the condition |
| **Source** | The subsystem or object that generated the alert |
| **Time** | Timestamp of the most recent occurrence |
| **Count** | Number of times this alert has been aggregated |
| **Dismiss button** | Removes the alert from the active list for this session |

---

## Filtering

The filter toolbar at the top of the Alerts tab controls which severity levels are shown:

| Filter | Shows |
|--------|-------|
| Info | Info only |
| Warning | Warning only |
| Critical | Critical only |
| (all active) | All non-dismissed alerts |

Dismissed alerts are hidden by default. Toggle **Show Dismissed** to include them.

---

## Alert Sources

Alerts are contributed by any class implementing `IAlertSource`. Built-in sources:

| Source | Alert conditions |
|--------|----------------|
| `CameraInspectorNode` | Clip ratio, depth conflicts, empty culling mask |
| `AudioInspectorNode` | Missing listener, multiple listeners, silent playing source |
| `PerformanceProfiler` | Slow frames, GC spikes |

Custom alert sources can be implemented. See [Custom Alert Source](../../guides/custom-alert-source.md).

---

## Stats Bar

The **Alerts** counter in the stats bar reflects the current count of non-dismissed alerts across all severity levels. The counter updates every editor frame.

---

## Report Export

All alerts (including dismissed) are included in exported session reports. See [Report Export](../../guides/report-export.md).
