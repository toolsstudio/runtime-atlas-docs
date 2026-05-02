# Installation
**Runtime Atlas v1.2.0**

---

## Obtaining the Package

Runtime Atlas is a paid product. Purchase it before following the import steps.

| Platform | Link |
|----------|------|
| Unity Asset Store | https://assetstore.unity.com/packages/slug/367424 |
| itch.io | https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit |
| Gumroad | https://toolsstudio.gumroad.com/l/runtime-atlas |

Source code is not included.

---

## Requirements

| Requirement | Value |
|-------------|-------|
| Unity minimum | 2021.3 LTS |
| Unity maximum tested | Unity 6.x (6000.x) |
| Render pipeline | Built-in, URP, HDRP |
| Input backend | Any — Input System and legacy Input Manager both supported |
| Editor platform | Windows, macOS, Linux |
| Player build impact | None — Editor-only assembly |

---

## Import

### From the Unity Asset Store

1. Open **Package Manager** (`Window > Package Manager`).
2. Select **My Assets**.
3. Locate **Runtime Atlas** and click **Import**.
4. Select all files in the import dialog and confirm.
5. Wait for Unity to complete script compilation.

### From itch.io or Gumroad

Purchases from itch.io and Gumroad deliver a `.unitypackage` file.

1. Download the `.unitypackage` from your purchase page.
2. In Unity: `Assets > Import Package > Custom Package`.
3. Select the downloaded file, select all files in the dialog, and confirm.
4. Wait for Unity to complete script compilation.

### Upgrading From a Previous Version

Delete `Assets/RuntimeAtlas` completely before importing the new version. Importing on top of an existing installation leaves stale files that cause issues. See the [Upgrade Guide](upgrade-guide.md) for version-specific steps.

---

## Validation

### Assembly Definitions Present

```
Assets/RuntimeAtlas/Runtime/RuntimeAtlas.Core.asmdef
Assets/RuntimeAtlas/Runtime/Demo/RuntimeAtlas.Core.Demo.asmdef
Assets/RuntimeAtlas/Editor/RuntimeAtlas.Editor.asmdef
Assets/RuntimeAtlas/Editor/Demo/RuntimeAtlas.Editor.Demo.asmdef
```

### Zero Compile Errors

The Unity Console must show no compile errors before proceeding. See [Troubleshooting](../troubleshooting.md) if errors appear.

### Window Opens and Shows Correct Version

1. `Window > Runtime Atlas > Open` (shortcut: `Ctrl+Alt+R`).
2. The window opens and docks normally.
3. The About tab and Project Settings page display **Version 1.2.0**.

---

## First Run

On first import, Runtime Atlas shows a one-time dialog. Dismiss with **OK**. It will not reappear.

---

## Settings Location

```
Assets/RuntimeAtlas/Editor/Resources/RuntimeAtlasSettings.asset
```

Access via **Edit > Project Settings > Runtime Atlas** or the gear icon (⚙) in the window header.

---

## Uninstall

Delete `Assets/RuntimeAtlas`. No files are written outside this folder. EditorPrefs use the `RuntimeAtlas.*` prefix and are safe to leave.
