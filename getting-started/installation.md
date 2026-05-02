# Installation

**Runtime Atlas v1.2.0**

---

## Obtaining the Package

Runtime Atlas is a paid product. Purchase before following these steps.

| Platform | Link |
|----------|------|
| Unity Asset Store | [Unity Asset Store](https://assetstore.unity.com/packages/slug/367424) |
| itch.io | [itch.io](https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit) |
| Gumroad | [Gumroad](https://toolsstudio.gumroad.com/l/runtime-atlas) |

Source code is not included.

---

## Requirements

| Requirement | Value |
|-------------|-------|
| Unity (minimum) | 2021.3 LTS |
| Unity (maximum tested) | Unity 6.x (6000.x) |
| Render pipeline | Built-in, URP, HDRP |
| Input backend | Any — Input System and legacy Input Manager both supported |
| Platform | Windows, macOS, Linux (Editor only) |
| Third-party packages | None |

Runtime Atlas is an Editor-only toolkit. It adds no overhead to player builds.

---

## Import

### From the Unity Asset Store

1. Open the Package Manager: `Window > Package Manager`.
2. Select **My Assets**.
3. Locate **Runtime Atlas** and click **Import**.
4. Import all files.
5. Let Unity complete script compilation. Expect one domain reload.

### From itch.io or Gumroad

1. Download the `.unitypackage` from your purchase page.
2. In Unity: `Assets > Import Package > Custom Package`.
3. Select the downloaded file and import all files.
4. Let Unity complete script compilation.

---

## Post-Import Validation

### Assembly Definitions

Verify these four files exist:

```
Assets/RuntimeAtlas/Runtime/RuntimeAtlas.Core.asmdef
Assets/RuntimeAtlas/Runtime/Demo/RuntimeAtlas.Core.Demo.asmdef
Assets/RuntimeAtlas/Editor/RuntimeAtlas.Editor.asmdef
Assets/RuntimeAtlas/Editor/Demo/RuntimeAtlas.Editor.Demo.asmdef
```

### Compile Check

Zero compile errors in the Unity Console. If errors appear, see [Troubleshooting](../troubleshooting.md).

### Window Opens

Open: `Window > Runtime Atlas > Open` or press `Ctrl+Alt+R`. The About tab must show **Version 1.2.0**.

---

## Settings Asset

Created automatically on first open at:

```
Assets/RuntimeAtlas/Editor/Resources/RuntimeAtlasSettings.asset
```

Do not move or delete this file. If missing, reopen the window to recreate it with default values.

---

## Uninstall

Delete `Assets/RuntimeAtlas`. No files are written outside this folder.

---

## Upgrading

See [Upgrade Guide](upgrade-guide.md).
