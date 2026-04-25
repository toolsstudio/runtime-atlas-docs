# Installation

**Runtime Atlas v1.1.0**

---

## Obtaining the Package

Runtime Atlas is a paid product. Purchase it from one of the following platforms
before following the import steps below.

| Platform | URL |
|----------|-----|
| Unity Asset Store | https://assetstore.unity.com/packages/slug/367424 |
| itch.io | https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit |
| Gumroad | https://toolsstudio.gumroad.com/l/runtime-atlas |

Source code is not included and is not publicly available.

---

## Requirements

| Requirement | Minimum |
|-------------|---------|
| Unity | 2021.3 LTS |
| Unity (maximum tested) | Unity 6.x (6000.x) |
| Render pipeline | Built-in, URP, HDRP |
| Input backend | Any (Input System and legacy Input Manager both supported) |
| Platform | Windows, macOS, Linux (Editor only) |

Runtime Atlas is an Editor-only toolkit. It has no runtime player dependencies
and adds no overhead to player builds.

---

## Import

### From the Unity Asset Store

1. Open the **Package Manager** (`Window > Package Manager`).
2. Select **My Assets**.
3. Locate **Runtime Atlas** and click **Import**.
4. In the import dialog, import all files.
5. Let Unity complete script compilation.

### From itch.io or Gumroad

Purchases on itch.io and Gumroad deliver a `.unitypackage` file.

1. Download the `.unitypackage` from your purchase page.
2. In Unity, open `Assets > Import Package > Custom Package`.
3. Select the downloaded `.unitypackage` file.
4. In the import dialog, import all files.
5. Let Unity complete script compilation.

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

The Unity Console must show no compile errors. If errors appear,
see [Troubleshooting](../troubleshooting.md).

### Window Opens

1. Open the window: `Window > Runtime Atlas > Open` or press `Ctrl+Alt+R`.
2. The Runtime Atlas window should appear and dock normally.
3. The header should display **Runtime Atlas** and **Version 1.1.0**.

---

## First Run

On first import, Runtime Atlas displays a one-time upgrade dialog confirming the
package is active. Click **OK** to dismiss. It will not appear again.

---

## Input System

Runtime Atlas core systems do not use Unity's input APIs. The demo scene includes
an input compatibility layer (`RADemoInputCompat`) that supports both legacy
Input Manager and the new Input System without requiring either to be present.
No configuration is needed.

---

## Uninstall

Delete the `Assets/RuntimeAtlas` folder from your project. No other files are
written outside this folder. EditorPrefs written by Runtime Atlas use the
`RuntimeAtlas.*` key prefix and are harmless to leave.

---

## Support

If import fails or you encounter licensing issues, reach out via:

- **Discord:** https://discord.gg/g5sNBZHZBd
- The support channel on the platform you purchased from
