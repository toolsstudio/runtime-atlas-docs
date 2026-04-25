# Alert System API

**Namespace:** `RuntimeAtlas` (types), `RuntimeAtlas.Editor` (system)  
**Assembly:** `RuntimeAtlas.Core` (types), `RuntimeAtlas.Editor` (system)  
**Runtime Atlas v1.1.0**

---

## Overview

The alert system is split across two layers:

- **Data types** (`RuntimeAtlas` namespace, ships in player build): `AlertSeverity`, `AlertEntry`
- **System** (`RuntimeAtlas.Editor` namespace, Editor only): `AlertSystem`, `IAlertSource`

---

## `AlertSeverity` enum

```csharp
namespace RuntimeAtlas

public enum AlertSeverity
{
    Info     = 0,
    Warning  = 1,
    Critical = 2
}
```

| Value | Meaning |
|-------|---------|
| `Info` | Informational. No user action required. |
| `Warning` | Condition that may cause unexpected behaviour. |
| `Critical` | Condition expected to cause a problem. |

---

## `AlertEntry` struct

```csharp
namespace RuntimeAtlas

public struct AlertEntry
```

| Member | Type | Description |
|--------|------|-------------|
| `Message` | `string` | Human-readable description |
| `Severity` | `AlertSeverity` | Severity level |
| `SourceName` | `string` | Name of the contributing system or object |
| `Timestamp` | `double` | Editor time at last occurrence |
| `GroupKey` | `string` | Aggregation key — entries with the same key are merged |
| `OccurrenceCount` | `int` | Number of times this alert has been raised and aggregated |
| `Dismissed` | `bool` | Whether the user has dismissed this entry |

### Constructor

```csharp
public AlertEntry(
    string message,
    AlertSeverity severity,
    string sourceName,
    double timestamp,
    string groupKey = null)
```

`groupKey` defaults to an empty string when `null`, disabling aggregation.

---

## `IAlertSource` interface

```csharp
namespace RuntimeAtlas.Editor

public interface IAlertSource
```

Implement this interface on any class that should contribute alerts to the Runtime Atlas alert system.

| Member | Description |
|--------|-------------|
| `string AlertSourceId { get; }` | Unique identifier for this source. Used as a default group key prefix. |
| `void EvaluateAlerts(AlertSystem alertSystem, double timestamp)` | Called by `AlertSystem.Evaluate()` each refresh cycle. Call `alertSystem.AddAlert(...)` for each condition detected. |

See [Custom Alert Source Guide](../guides/custom-alert-source.md) for a complete implementation example.

---

## `AlertSystem` class

```csharp
namespace RuntimeAtlas.Editor

public sealed class AlertSystem
```

Manages the alert list. Handles aggregation, filtering, and dismissal.

### Properties

| Property | Type | Description |
|----------|------|-------------|
| `AllAlerts` | `IReadOnlyList<AlertEntry>` | All alerts including dismissed. Used for report export. |
| `Count` | `int` | Non-dismissed alert count across all severities |
| `CriticalCount` | `int` | Non-dismissed critical alert count |

### Methods

```csharp
// Add an alert. Repeated calls with the same groupKey and within
// minIntervalSeconds are aggregated into one entry.
public void AddAlert(
    string message,
    AlertSeverity severity,
    string sourceName,
    double timestamp)

public void AddAlert(
    string message,
    AlertSeverity severity,
    string sourceName,
    double timestamp,
    string groupKey,
    double minIntervalSeconds)
```

| Parameter | Description |
|-----------|-------------|
| `message` | Alert description text |
| `severity` | `AlertSeverity` level |
| `sourceName` | Display name of the contributing system |
| `timestamp` | `EditorApplication.timeSinceStartup` at the time of the event |
| `groupKey` | Optional aggregation key. Alerts with the same key are merged. |
| `minIntervalSeconds` | Minimum seconds between new occurrences of the same group key. |

```csharp
// Evaluate all registered IAlertSource implementations.
public void Evaluate(IEnumerable<IAlertSource> sources, double timestamp)

// Remove all alerts.
public void Clear()

// Dismiss all current alerts.
public void DismissAll()
```
