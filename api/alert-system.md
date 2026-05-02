# Alert System API

**Namespace:** `RuntimeAtlas` (types) | `RuntimeAtlas.Editor` (system)  
**Assembly:** `RuntimeAtlas.Core` (types) | `RuntimeAtlas.Editor` (system)  
**Runtime Atlas v1.2.0**

---

## Overview

The alert system is split across two layers:

| Layer | Namespace | Assembly | Ships in player |
|-------|-----------|----------|----------------|
| Data types | `RuntimeAtlas` | `RuntimeAtlas.Core` | Yes |
| System | `RuntimeAtlas.Editor` | `RuntimeAtlas.Editor` | No |

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
| `Info` | Informational. No action required. |
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
| `Timestamp` | `double` | Editor time at last occurrence (`EditorApplication.timeSinceStartup`) |
| `GroupKey` | `string` | Aggregation key — entries with the same key are merged |
| `OccurrenceCount` | `int` | Number of times this entry has been aggregated |
| `Dismissed` | `bool` | Whether the user has dismissed this entry |

### Constructor

```csharp
public AlertEntry(
    string        message,
    AlertSeverity severity,
    string        sourceName,
    double        timestamp,
    string        groupKey = null)
```

`groupKey` defaults to an empty string when `null`, which disables aggregation (each call creates a new entry).

---

## `IAlertSource` interface

```csharp
namespace RuntimeAtlas.Editor

public interface IAlertSource
{
    string AlertSourceId { get; }
    void EvaluateAlerts(AlertSystem alertSystem, double timestamp);
}
```

| Member | Description |
|--------|-------------|
| `AlertSourceId` | Unique string identifier for this source. Use as a prefix for group keys to prevent collisions with other sources. |
| `EvaluateAlerts` | Called by `AlertSystem.Evaluate()` each refresh cycle. Call `alertSystem.AddAlert(...)` for each condition detected. |

See [Custom Alert Source](../guides/custom-alert-source.md) for a complete implementation example.

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
| `CriticalCount` | `int` | Non-dismissed Critical-severity count |

### Methods

```csharp
// Add an alert. Calls with the same groupKey within minIntervalSeconds
// are aggregated — OccurrenceCount increments rather than a new entry being created.
public void AddAlert(
    string        message,
    AlertSeverity severity,
    string        sourceName,
    double        timestamp)

public void AddAlert(
    string        message,
    AlertSeverity severity,
    string        sourceName,
    double        timestamp,
    string        groupKey,
    double        minIntervalSeconds)
```

| Parameter | Description |
|-----------|-------------|
| `message` | Alert description text |
| `severity` | `AlertSeverity` level |
| `sourceName` | Display name of the contributing system |
| `timestamp` | `EditorApplication.timeSinceStartup` at event time |
| `groupKey` | Aggregation key. Alerts with the same key and within `minIntervalSeconds` are merged. |
| `minIntervalSeconds` | Minimum seconds between new occurrences under the same `groupKey`. |

```csharp
// Evaluate all registered IAlertSource implementations.
public void Evaluate(IEnumerable<IAlertSource> sources, double timestamp)

// Remove all alerts.
public void Clear()

// Dismiss all current alerts.
public void DismissAll()
```
