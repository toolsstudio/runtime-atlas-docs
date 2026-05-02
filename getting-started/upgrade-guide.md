# Upgrade Guide
**Runtime Atlas**

> This guide is for licensed customers upgrading between versions.
> If you have not yet installed Runtime Atlas, see [Installation](installation.md).

---

## General Upgrade Procedure

For all version upgrades:

1. Close the Runtime Atlas window in Unity.
2. Delete `Assets/RuntimeAtlas` from your project.
3. Import the new version (Asset Store, itch.io, or Gumroad).
4. Confirm zero compile errors in the Console.
5. Open `Window > Runtime Atlas > Open` and verify the About tab shows the new version.

Do not import a new version on top of an existing installation.

---

## v1.1.0 → v1.2.0

**Breaking changes:** None.

**API changes:** None. No public types, method signatures, or interfaces changed.

**What changed:** v1.2.0 is a stabilization release. All changes are internal — GUIStyle caching, texture lifecycle fixes, and FindObjectsByType throttling. No migration steps are required.

**Verification after upgrade:**

1. Open the Unity Console. Confirm zero compile errors.
2. Open `Window > Runtime Atlas > Open`.
3. Confirm the About tab shows **Version 1.2.0**.
4. Enter Play Mode and confirm Camera, Audio, Physics, and Profiler tabs populate normally.

---

## v1.0.0 → v1.1.0

### Breaking Change: Namespace Migration

All public Runtime Atlas types moved to new namespaces.

| Previous | New |
|----------|-----|
| `Arish.RA` | `RuntimeAtlas` |
| `Arish.RA.Editor` | `RuntimeAtlas.Editor` |

Affected types:

| Type | Previous namespace | New namespace |
|------|--------------------|----|
| `AlertEntry` | `Arish.RA` | `RuntimeAtlas` |
| `AlertSeverity` | `Arish.RA` | `RuntimeAtlas` |
| All Editor classes | `Arish.RA.Editor` | `RuntimeAtlas.Editor` |

### Migration Steps

**Step 1 — Update `using` directives**

```csharp
// Before
using Arish.RA;
using Arish.RA.Editor;

// After
using RuntimeAtlas;
using RuntimeAtlas.Editor;
```

**Step 2 — Update fully-qualified type references (if any)**

```csharp
// Before
Arish.RA.AlertEntry entry = new Arish.RA.AlertEntry(...);

// After
RuntimeAtlas.AlertEntry entry = new RuntimeAtlas.AlertEntry(...);
```

**Step 3 — Assembly definition references**

Assembly names (`RuntimeAtlas.Core`, `RuntimeAtlas.Editor`) have not changed. If your custom `.asmdef` files reference these assemblies by name, no change is needed.

**Step 4 — Re-import**

Delete `Assets/RuntimeAtlas` and import the v1.1.0 package. The package bootstrap detects the previous installation and migrates the relevant EditorPrefs key automatically.

### Verification

1. Open the Unity Console. Confirm zero compile errors.
2. Open `Window > Runtime Atlas > Open`.
3. Confirm the About tab shows **Version 1.1.0**.
4. If the demo scene is in use, open it and enter Play Mode. Confirm zero missing-script warnings.
