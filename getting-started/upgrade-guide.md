# Upgrade Guide — v1.0.0 to v1.1.0

**Runtime Atlas v1.1.0**

> This guide is for licensed customers upgrading from v1.0.0.
> If you have not yet purchased Runtime Atlas, see
> [Installation](installation.md) for purchase and import instructions.

---

## Breaking Changes

Version 1.1.0 contains one breaking change: a full namespace rename.

### Namespace Migration

All public Runtime Atlas types have moved to new namespaces.

| Previous namespace | New namespace |
|-------------------|--------------|
| `Arish.RA` | `RuntimeAtlas` |
| `Arish.RA.Editor` | `RuntimeAtlas.Editor` |

**Affected public types:**

| Type | Previous namespace | New namespace |
|------|--------------------|--------------|
| `AlertEntry` | `Arish.RA` | `RuntimeAtlas` |
| `AlertSeverity` | `Arish.RA` | `RuntimeAtlas` |
| All Editor classes | `Arish.RA.Editor` | `RuntimeAtlas.Editor` |

---

## Migration Steps

### 1. Update `using` directives

In any project script that references Runtime Atlas types, replace:

```csharp
// Before
using Arish.RA;
using Arish.RA.Editor;
```

```csharp
// After
using RuntimeAtlas;
using RuntimeAtlas.Editor;
```

### 2. Update fully-qualified type references

If your code uses fully qualified names (without `using` directives), update accordingly:

```csharp
// Before
Arish.RA.AlertEntry entry = new Arish.RA.AlertEntry(...);
Arish.RA.AlertSeverity sev = Arish.RA.AlertSeverity.Warning;
```

```csharp
// After
RuntimeAtlas.AlertEntry entry = new RuntimeAtlas.AlertEntry(...);
RuntimeAtlas.AlertSeverity sev = RuntimeAtlas.AlertSeverity.Warning;
```

### 3. Update Assembly Definition references

If any custom `.asmdef` in your project explicitly references `RuntimeAtlas.Core` or `RuntimeAtlas.Editor`, no change is needed — these assembly names have not changed, only the C# namespaces inside them.

### 4. Re-import the package

After updating directives, delete `Assets/RuntimeAtlas` and re-import the v1.1.0 package. The package bootstrap will detect the previous installation and migrate the relevant EditorPrefs key automatically.

---

## Non-Breaking Changes in 1.1.0

These changes require no action from existing users:

- Demo scene script bindings are repaired. If you were seeing missing-script warnings on demo scene objects, they are resolved.
- The Add Component button in the Inspector tab no longer logs a console error in Unity 6.
- The `RuntimeAtlas.Editor` assembly no longer references `RuntimeAtlas.Core.Demo`. If you had a custom assembly referencing `RuntimeAtlas.Editor`, this change has no effect on your project.

---

## Verification After Upgrade

1. Open the Unity Console. Confirm zero compile errors.
2. Open `Window > Runtime Atlas > Open`.
3. Confirm the About tab shows **Version 1.1.0**.
4. If the demo scene is in use, open it and enter Play Mode. Confirm zero missing-script warnings.
