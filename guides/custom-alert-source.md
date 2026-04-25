# Custom Alert Source

**Runtime Atlas v1.1.0**

---

## Overview

Any class can contribute alerts to the Runtime Atlas alert system by implementing `IAlertSource`. This decouples custom diagnostic logic from the built-in inspector nodes and keeps the alert system extensible without modifying package code.

---

## Interface

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
| `AlertSourceId` | A unique string identifier for this source. Used as a prefix for group keys to prevent collisions with other sources. |
| `EvaluateAlerts` | Called by the alert system on each evaluation cycle. Add alerts by calling `alertSystem.AddAlert(...)`. |

---

## Implementation

The following example monitors a custom game system and raises alerts based on its state.

```csharp
using UnityEditor;
using RuntimeAtlas.Editor;

public sealed class NetworkDiagnosticsAlertSource : IAlertSource
{
    public string AlertSourceId => "NetworkDiagnostics";

    public void EvaluateAlerts(AlertSystem alertSystem, double timestamp)
    {
        // Example: read state from your system and raise alerts as needed.
        // Replace the condition below with real diagnostic logic.

        int droppedPackets = GetDroppedPacketCount();
        if (droppedPackets > 10)
        {
            alertSystem.AddAlert(
                message:           $"High packet drop rate: {droppedPackets} dropped",
                severity:          AlertSeverity.Warning,
                sourceName:        "Network",
                timestamp:         timestamp,
                groupKey:          $"{AlertSourceId}.HighPacketDrop",
                minIntervalSeconds: 3.0
            );
        }

        bool serverUnreachable = IsServerUnreachable();
        if (serverUnreachable)
        {
            alertSystem.AddAlert(
                message:           "Server connection lost",
                severity:          AlertSeverity.Critical,
                sourceName:        "Network",
                timestamp:         timestamp,
                groupKey:          $"{AlertSourceId}.ServerUnreachable",
                minIntervalSeconds: 5.0
            );
        }
    }

    private int GetDroppedPacketCount() => 0;   // replace with real implementation
    private bool IsServerUnreachable()  => false; // replace with real implementation
}
```

---

## Registering the Source

Custom sources must be registered with the `AlertSystem` instance. The cleanest approach is to hook into the Runtime Atlas window's evaluation cycle from an `[InitializeOnLoad]` class.

```csharp
using UnityEditor;
using RuntimeAtlas.Editor;

[InitializeOnLoad]
public static class NetworkDiagnosticsRegistrar
{
    private static readonly NetworkDiagnosticsAlertSource s_Source
        = new NetworkDiagnosticsAlertSource();

    static NetworkDiagnosticsRegistrar()
    {
        RASettings.OnAlertSourcesRequested += RegisterSources;
    }

    private static void RegisterSources(System.Collections.Generic.List<IAlertSource> sources)
    {
        sources.Add(s_Source);
    }
}
```

If `RASettings.OnAlertSourcesRequested` is not available in the version you are using, register directly through the `AlertSystem` reference obtained from `AtlasWindow.AlertSystem` (access the window via `EditorWindow.GetWindow<AtlasWindow>()`).

---

## Evaluation Cycle

`EvaluateAlerts` is called:

- Each editor update tick while Play Mode is active and the Runtime Atlas window is open.
- Once per frame during the window's repaint cycle in Edit Mode.

The method must be fast. Avoid allocations, file I/O, or reflection inside `EvaluateAlerts`. Cache any necessary references in the class constructor or in a separate `Update`-style method.

---

## Group Keys

The `groupKey` parameter controls alert aggregation. Two calls to `AddAlert` with the same `groupKey` within `minIntervalSeconds` increment the `OccurrenceCount` of the existing entry rather than adding a new one.

Best practice: prefix your group keys with `AlertSourceId` to prevent collisions with built-in sources.

```csharp
groupKey: $"{AlertSourceId}.MyConditionName"
```

---

## Severity Guidelines

| Condition type | Recommended severity |
|----------------|---------------------|
| Informational state worth noting | `Info` |
| Degraded performance or unexpected configuration | `Warning` |
| Failure that will produce incorrect behaviour | `Critical` |
