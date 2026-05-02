# Alert System API
**Runtime Atlas v1.2.0**

---

## Assemblies

| Type | Assembly | Namespace |
|------|----------|-----------|
| `AlertSeverity` | `RuntimeAtlas.Core` | `RuntimeAtlas` |
| `AlertEntry` | `RuntimeAtlas.Core` | `RuntimeAtlas` |
| `AlertSystem` | `RuntimeAtlas.Editor` | `RuntimeAtlas.Editor` |
| `IAlertSource` | `RuntimeAtlas.Editor` | `RuntimeAtlas.Editor` |

---

## AlertSeverity

```csharp
public enum AlertSeverity
{
    Info,
    Warning,
    Critical
}
```

Used to classify alert entries. Maps directly to the badge colours in the Alerts tab: Info = blue, Warning = yellow, Critical = red.

---

## AlertEntry

```csharp
public sealed class AlertEntry
{
    public string      Message    { get; }
    public AlertSeverity Severity { get; }
    public string      Source     { get; }
    public int         Count      { get; }
    public bool        Dismissed  { get; }
}
```

| Property | Description |
|----------|-------------|
| `Message` | Alert description text |
| `Severity` | `Info`, `Warning`, or `Critical` |
| `Source` | Label identifying which module generated the alert |
| `Count` | Number of times this message was added since last cleared |
| `Dismissed` | Whether the user has dismissed this entry |

`AlertEntry` instances are owned by `AlertSystem`. They should not be constructed directly.

---

## AlertSystem

```csharp
public sealed class AlertSystem
```

**Adding alerts:**

```csharp
public void AddAlert(string message, AlertSeverity severity, string source);
```

Adds an alert to the log. If an alert with the same `message` and `source` already exists and is not dismissed, its `Count` is incremented rather than adding a duplicate entry.

**Reading alerts:**

```csharp
public IReadOnlyList<AlertEntry> Alerts { get; }
```

Returns all alerts (including dismissed ones). Filter on `Dismissed` to show only active alerts.

**Dismissing alerts:**

```csharp
public void Dismiss(AlertEntry entry);
public void DismissAll();
public void ClearDismissed();
```

| Method | Effect |
|--------|--------|
| `Dismiss(entry)` | Sets `entry.Dismissed = true` |
| `DismissAll()` | Sets `Dismissed = true` on all entries |
| `ClearDismissed()` | Permanently removes all dismissed entries |

**Clearing:**

```csharp
public void Clear();
```

Removes all entries, dismissed or not.

**Registering sources:**

```csharp
public void RegisterSource(IAlertSource source);
public void UnregisterSource(IAlertSource source);
```

Registered sources have their `EvaluateAlerts` method called on each update cycle.

---

## IAlertSource

```csharp
public interface IAlertSource
{
    void EvaluateAlerts(AlertSystem alertSystem);
}
```

Implement to contribute project-specific alerts. See [Custom Alert Source](../guides/custom-alert-source.md) for a complete implementation example.

`EvaluateAlerts` is called on `EditorApplication.update`. Treat it as a hot path — avoid `FindObjectsByType` on every call without throttling.
