# Installation

**Runtime Atlas v1.1.0**

---

## Requirements

| Requirement | Minimum |
|-------------|---------|
| Unity | 2021.3 LTS |
| Unity (maximum tested) | Unity 6.x (6000.x) |
| Render pipeline | Built-in, URP, HDRP |
| Input backend | Any (Input System and legacy Input Manager both supported) |
| Platform | Windows, macOS, Linux (Editor only) |

Runtime Atlas is an Editor-only toolkit. It has no runtime player dependencies and adds no overhead to player builds.

---

## Import

### From Unity Asset Store

1. Open the **Package Manager** (`Window > Package Manager`).
2. Select **My Assets**.
3. Locate **Runtime Atlas** and click **Import**.
4. In the import dialog, import all files.
5. Let Unity complete script compilation.

### Manual Import

1. Copy the `Assets/RuntimeAtlas` folder into your project's `Assets` directory.
2. Let Unity complete script compilation.

---

## Validation

After import, confirm the following before opening the window.

### Assembly Definitions

Verify these files exist in the Project window:

```
Assets/RuntimeAtlas/Runtime/RuntimeAtlas.Core.asmdef
Assets/RuntimeAtlas/Runtime/Demo/RuntimeAtlas.Core.Demo.asmdef
Assets/RuntimeAtlas/Editor/RuntimeAtlas.Editor.asmdef
Assets/RuntimeAtlas/Editor/Demo/RuntimeAtlas.Editor.Demo.asmdef
```

### No Compile Errors

The Unity Console must show no compile errors. If errors appear, see [Troubleshooting](../troubleshooting.md).

### Window Opens

1. Open the window: `Window > Runtime Atlas > Open` or press `Ctrl+Alt+R`.
2. The Runtime Atlas window should appear and dock normally.
3. The header should display **Runtime Atlas** and **Version 1.1.0**.

---

## First Run

On first import, Runtime Atlas displays a one-time upgrade dialog. This dialog confirms the package is active. Click **OK** to dismiss it. It will not appear again.

To re-open it manually, delete the `RuntimeAtlas.Upgrade.1.0.0.EditorUX` key from **Edit > Preferences > (any)** — though there is no reason to do so under normal circumstances.

---

## Input System

Runtime Atlas core systems do not use Unity's input APIs. The demo scene includes an input compatibility layer (`RADemoInputCompat`) that supports both legacy Input Manager and the new Input System without requiring either to be present. No configuration is needed.

---

## Uninstall

Delete the `Assets/RuntimeAtlas` folder from your project. No other files are written outside this folder. EditorPrefs written by Runtime Atlas use the `RuntimeAtlas.*` key prefix and are harmless to leave.
