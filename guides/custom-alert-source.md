# Custom Alert Source
**Runtime Atlas v1.2.0**

---

## Overview

The `IAlertSource` interface allows any class to contribute alerts to the Runtime Atlas `AlertSystem`. Implementing it in your own editor code is the supported extension point for adding project-specific diagnostic alerts.

---

## Interface

```csharp
// Namespace: RuntimeAtlas.Editor
// File: Assets/RuntimeAtlas/Editor/Alerts/IAlertSource.cs

public interface IAlertSource
{
    void EvaluateAlerts(AlertSystem alertSystem);
}
```

`EvaluateAlerts` is called once per update cycle. The implementation should inspect scene state and call `alertSystem.AddAlert(...)` for any conditions it detects.

---

## AlertSystem API

```csharp
public void AddAlert(string message, AlertSeverity severity, string source);
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `message` | `string` | Human-readable alert description |
| `severity` | `AlertSeverity` | `Info`, `Warning`, or `Critical` |
| `source` | `string` | Label shown in the Alerts tab Source column |

---

## AlertSeverity Enum

```csharp
// Namespace: RuntimeAtlas
// File: Assets/RuntimeAtlas/Runtime/AlertEntry.cs

public enum AlertSeverity
{
    Info,
    Warning,
    Critical
}
```

---

## Example Implementation

```csharp
using RuntimeAtlas;
using RuntimeAtlas.Editor;
using UnityEditor;
using UnityEngine;

public class MyAlertSource : IAlertSource
{
    public void EvaluateAlerts(AlertSystem alertSystem)
    {
        // Example: flag if there are more than 10 active lights
#if UNITY_2022_2_OR_NEWER
        var lights = Object.FindObjectsByType<Light>(FindObjectsSortMode.None);
#else
        var lights = Object.FindObjectsOfType<Light>();
#endif
        int activeCount = 0;
        foreach (var l in lights)
            if (l != null && l.isActiveAndEnabled) activeCount++;

        if (activeCount > 10)
        {
            alertSystem.AddAlert(
                $"{activeCount} active lights detected. Consider reducing for performance.",
                AlertSeverity.Warning,
                "MyAlertSource"
            );
        }
    }
}
```

---

## Registration

`IAlertSource` implementations must be registered with `AlertSystem`. The registration point depends on how your editor code is structured.

If you are adding alerts from an `EditorWindow` or editor utility class, register in `OnEnable` and deregister in `OnDisable`:

```csharp
// In your EditorWindow or editor utility
private MyAlertSource _myAlertSource;

private void OnEnable()
{
    _myAlertSource = new MyAlertSource();
    // AlertSystem is accessed via the AtlasWindow instance —
    // see AlertSystem API documentation for the registration method.
}
```

**Note:** The specific registration API on `AlertSystem` depends on how your project references the Runtime Atlas editor assembly. See [Alert System API](../api/alert-system.md) for the full `AlertSystem` public surface.

---

## Design Notes

- `EvaluateAlerts` is called on `EditorApplication.update` — treat it as a hot path. Cache scene queries; do not call `FindObjectsByType` on every invocation.
- Duplicate alert messages within the same evaluation cycle are aggregated (count incremented), not duplicated in the list.
- Alerts persist until dismissed. Your source should not add the same alert repeatedly unless the condition has genuinely changed.
