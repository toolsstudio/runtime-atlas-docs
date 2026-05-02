# Upgrade Guide

**Runtime Atlas v1.2.0**

---

## v1.1.0 → v1.2.0

### Breaking Changes

None. v1.2.0 is a production polish release — no public API changes, no namespace changes, no module boundary changes.

### What Changed

- All `.cs` file headers updated to `Version 1.2.0`. No code impact.
- Hot-path `GUIContent` allocations eliminated in `ScriptViewerWindow`, `ComponentInspectorPanel`, `AnimatorMonitor`, and `AudioMixerPanel`. No API or behaviour change — internal caching only.
- IMGUI layout stack corruption fixed in `AtlasWindow.DrawActiveTabSafely`. No UI or behaviour change; only the error recovery path is improved.
- `RADemoController` texture HideFlags fix. No visible behaviour change.

### Migration Steps

No migration steps required. Delete `Assets/RuntimeAtlas` and re-import the v1.2.0 package.

### Verification

1. Open the Unity Console. Confirm zero compile errors.
2. Open `Window > Runtime Atlas > Open`.
3. Confirm the About tab shows **Version 1.2.0**.

---

## v1.0.0 → v1.1.0

### Breaking Changes

Version 1.1.0 contains one breaking change: a full namespace rename.

**All public Runtime Atlas types moved namespaces:**

| Previous namespace | New namespace |
|-------------------|--------------|
| `Arish.RA` | `RuntimeAtlas` |
| `Arish.RA.Editor` | `RuntimeAtlas.Editor` |

**Affected public types:**

| Type | Previous namespace | New namespace |
|------|-------------------|--------------| 
| `AlertEntry` | `Arish.RA` | `RuntimeAtlas` |
| `AlertSeverity` | `Arish.RA` | `RuntimeAtlas` |
| All editor classes | `Arish.RA.Editor` | `RuntimeAtlas.Editor` |

### Migration Steps

**1. Update `using` directives**

```csharp
// Before
using Arish.RA;
using Arish.RA.Editor;

// After
using RuntimeAtlas;
using RuntimeAtlas.Editor;
```

**2. Update fully-qualified type references**

```csharp
// Before
Arish.RA.AlertEntry entry = new Arish.RA.AlertEntry(...);
Arish.RA.AlertSeverity sev = Arish.RA.AlertSeverity.Warning;

// After
RuntimeAtlas.AlertEntry entry = new RuntimeAtlas.AlertEntry(...);
RuntimeAtlas.AlertSeverity sev = RuntimeAtlas.AlertSeverity.Warning;
```

**3. Assembly Definition references**

Assembly names have not changed — only C# namespaces changed. If a custom `.asmdef` references `RuntimeAtlas.Core` or `RuntimeAtlas.Editor` by name, no change is needed.

**4. Re-import the package**

Delete `Assets/RuntimeAtlas` and re-import the v1.1.0 package. The package bootstrap detects the previous installation and migrates the relevant EditorPrefs key automatically.

### Verification After Upgrade

1. Open the Unity Console. Confirm zero compile errors.
2. Open `Window > Runtime Atlas > Open`.
3. Confirm the About tab shows **Version 1.1.0** (or **Version 1.2.0** if upgrading further).
4. Open the demo scene and enter Play Mode. Confirm zero missing-script warnings.
