# Troubleshooting
**Runtime Atlas v1.2.0**

---

## Compile Errors After Import

**Symptom:** Unity Console shows compile errors immediately after importing.

**Resolution:**

1. Check the error message for the namespace. If it references `Arish.RA` or `Arish.RA.Editor`, you have project code referencing the pre-v1.1.0 namespace. See the [Upgrade Guide](getting-started/upgrade-guide.md) for migration steps.
2. If errors reference `RuntimeAtlas.*` types in your own scripts, verify your assembly definition files reference `RuntimeAtlas.Core` or `RuntimeAtlas.Editor` as appropriate.
3. If errors are inside the `Assets/RuntimeAtlas` folder itself, delete the folder and re-import the package from the source you purchased from.

---

## Window Does Not Open

**Symptom:** `Window > Runtime Atlas > Open` does nothing, or the item is missing from the menu.

**Resolution:**

1. Confirm there are zero compile errors in the Console. The menu item is registered during compilation — if compilation fails, the menu will not appear.
2. If the menu item is present but clicking it does nothing, reset the Unity window layout: `Window > Layouts > Default`.
3. If the issue persists, delete `Assets/RuntimeAtlas` and re-import.

---

## Window Shows "Version 1.1.0" After Upgrading to 1.2.0

**Symptom:** The About tab or Settings page displays the old version string.

**Resolution:**

This indicates a stale import. The old files are still present alongside the new ones. Delete `Assets/RuntimeAtlas` entirely, then re-import the v1.2.0 package. Do not import on top of an existing installation without deleting first.

---

## No Data in Camera / Audio / Physics Tabs

**Symptom:** Tabs show "No [cameras/sources/bodies] detected" during Play Mode.

**Resolution:**

1. Confirm you are in Play Mode. These tabs populate from live scene data and show limited information in Edit Mode.
2. Confirm the scene has the expected components. Camera tab requires `Camera` components in the scene; Audio tab requires `AudioSource` components; Physics tab requires `Rigidbody` components.
3. Confirm the Runtime Atlas window is visible and not minimized during Play Mode — the window pauses data collection when it is not visible.

---

## Edit Mode Shows Stale Object List (Camera / Audio / Animator)

**Symptom:** In Edit Mode, the Camera, Audio, or Animator tab continues to show objects that have been deleted or does not show newly added objects.

**Resolution:**

By design, edit-mode scene queries are throttled to once per second to prevent editor frame spikes. Wait approximately one second for the list to refresh. If objects persist longer than two seconds, this is unexpected — report via Discord.

---

## Alerts Tab Shows No Alerts During Play Mode

**Symptom:** You expect diagnostic alerts (e.g., multiple AudioListeners) but the Alerts tab is empty.

**Resolution:**

1. Confirm alerts are not filtered out. Open the Alerts tab and check the severity filter buttons in the toolbar. All severities (Info, Warning, Critical) should be toggled on.
2. Confirm the alert is not already dismissed. Dismissed alerts are hidden. Click **Clear Dismissed** to restore them.
3. Check the alert threshold settings. Open **Edit > Project Settings > Runtime Atlas** and review the configured thresholds.

---

## Script Scanner Finds No Results

**Symptom:** Clicking **Scan Scripts** in the Scanner tab returns zero results.

**Resolution:**

1. Confirm the search path is set correctly. The Scanner searches `Assets/` by default. If your scripts are outside this path, update the path in the Scanner tab settings.
2. Confirm you have `.cs` files in the search path. The scanner only processes C# source files.
3. The scanner is a static pattern analyser. It does not detect issues in files with zero matching patterns. An empty result means no matching patterns were found in the scanned files — it does not indicate a malfunction.

---

## Report Export Fails

**Symptom:** Clicking **Export** in the Report tab produces no file, or the file is empty.

**Resolution:**

1. Confirm you clicked **Generate Preview** before **Export**. The export requires a generated report — it cannot export empty state.
2. Confirm the destination folder is writable. Unity's file dialog defaults to the project root — check that you have write permissions to the selected folder.
3. For DOCX export specifically: DOCX generation uses `System.IO.Compression`. If the target platform is set to WebGL, this API may be restricted. Switch to Standalone or keep the editor target as Desktop.

---

## Demo Scene Objects Missing Scripts

**Symptom:** Opening `Assets/RuntimeAtlas/Demo/Scene/RA.unity` shows missing-script warnings on demo objects.

**Resolution:**

This was a known issue in v1.0.0, resolved in v1.1.0. If you are seeing it on v1.2.0, the demo scene file from v1.0.0 may still be present in your project. Delete `Assets/RuntimeAtlas` and re-import the v1.2.0 package. The demo scene will be replaced with a clean version containing no missing-script references.

---

## Input System Warning: "Input Manager marked for deprecation"

**Symptom:** Unity shows a warning in the Console about Input Manager deprecation.

**Resolution:**

This warning is from Unity itself, not from Runtime Atlas. Runtime Atlas core systems do not use Unity's input APIs. The demo scene includes `RADemoInputCompat.cs`, which conditionally supports both legacy Input Manager and the new Input System. The warning does not affect Runtime Atlas functionality. To suppress it, either enable the new Input System in **Edit > Project Settings > Player** or disable the legacy Input Manager.

---

## Editor Lag or Freezing When Runtime Atlas Window Is Open

**Symptom:** The Unity Editor becomes sluggish while Runtime Atlas is open, especially with large scenes.

**Resolution:**

In v1.2.0, all `FindObjectsByType` calls from the UI layer are throttled to at most once per second. All `GUIStyle` objects are cached. If you are experiencing lag on v1.2.0 specifically:

1. Confirm you are on v1.2.0. Open the About tab and verify the version string. If it reads `Version 1.1.0`, see the stale import issue above.
2. Check if the Physics tab's Layer Matrix view is open — this view iterates all 32 physics layers per repaint. On scenes with many configured layers this can be slower than other tabs. Collapsing this view while not in use reduces repaint cost.
3. If the Scene tab is open with a very large scene (1,000+ objects), the object list rebuild can be slow. This is a known limitation. The Scene tab search field can be used to filter to a subset of objects.

---

## EditorPrefs Are Not Cleared After Uninstall

**Symptom:** After deleting `Assets/RuntimeAtlas`, some Editor preferences persist.

**Resolution:**

This is by design. EditorPrefs are stored in the OS user profile, not in the project folder, and are not deleted when a package is removed. Runtime Atlas uses keys with the `RuntimeAtlas.*` prefix. These are harmless to leave in place. To remove them manually, use `EditorPrefs.DeleteKey("RuntimeAtlas.<key>")` in a temporary editor script, or clear all EditorPrefs from the Unity Preferences window.
