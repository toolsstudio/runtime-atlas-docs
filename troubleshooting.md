# Troubleshooting

**Runtime Atlas v1.2.0**

---

## Compile Errors on Import

**Symptom:** Unity Console shows compile errors immediately after import.

| Cause | Fix |
|-------|-----|
| Existing code using `Arish.RA` namespace | Replace `using Arish.RA;` with `using RuntimeAtlas;` and `using Arish.RA.Editor;` with `using RuntimeAtlas.Editor;`. See [Upgrade Guide](getting-started/upgrade-guide.md). |
| Duplicate assembly definition from a prior import | Delete `Assets/RuntimeAtlas` fully before re-importing. Do not merge old and new packages. |
| Unity version below minimum | Runtime Atlas requires Unity 2021.3 LTS or later. |

---

## Window Does Not Appear

**Symptom:** `Window > Runtime Atlas` menu is missing, or clicking **Open** has no effect.

1. Confirm the import completed with zero compile errors. Errors prevent `[MenuItem]` attributes from registering.
2. Force a recompile: **Assets > Reimport All**, or delete the `Library/` folder and reopen the project.
3. Confirm `RuntimeAtlas.Editor.asmdef` exists at `Assets/RuntimeAtlas/Editor/RuntimeAtlas.Editor.asmdef`.

---

## IMGUI Layout Errors in Console

**Symptom:** Console shows `EndLayoutGroup: BeginLayoutGroup must be called first` or `InvalidOperationException: Stack empty`, both pointing to `AtlasWindow.OnGUI`.

**Cause in v1.1.0:** A module's `DrawGUI()` opened IMGUI layout groups and then threw an exception before closing them, corrupting the layout stack.

**Fix:** This is resolved in v1.2.0. `DrawActiveTabSafely` now wraps each module in a `BeginVertical`/`EndVertical` buffer and calls `GUIUtility.ExitGUI()` on exception to force a clean layout stack on the next repaint. Upgrade to v1.2.0.

---

## Missing Script Warnings in Demo Scene

**Symptom:** Yellow warning triangles on demo scene GameObjects; `The referenced script (Unknown) on behaviour is missing` in the Console.

**Cause:** Occurred in v1.0.0 due to an incomplete `.meta` file for the multi-class demo behaviour file.

**Fix:** Resolved in v1.1.0. Ensure you are running v1.1.0 or later. When upgrading from v1.0.0, delete `Assets/RuntimeAtlas` fully before re-importing.

---

## ExecuteMenuItem Console Error (Add Component Button)

**Symptom:** Console shows `ExecuteMenuItem target for Scripts does not exist` when clicking **+ Add Component** in the Inspector tab.

**Cause:** Occurred in v1.0.0 on Unity 6. The `Component/Scripts` menu path was removed in Unity 6.

**Fix:** Resolved in v1.1.0. Upgrade to v1.1.0 or later.

---

## Runtime Atlas Console Shows No Messages

**Symptom:** The Console tab shows `No messages captured yet` during active Play Mode.

**Explanation:** By design. The Runtime Atlas Console captures only messages that begin with `[RA]`, `[Runtime Atlas]`, or `[RuntimeAtlas]`. It does not mirror all Unity Console output.

To emit a capturable message:

```csharp
Debug.Log("[RA] My diagnostic message");
Debug.LogWarning("[Runtime Atlas] High GC alloc detected");
```

---

## Stats Bar Shows Zero Cameras or Sources

**Symptom:** Stats bar shows `Cameras: 0` or `Sources: 0` during Play Mode.

**Cause:** Components instantiated via prefab or inactive at the first poll cycle may not be counted immediately.

**Fix:** Wait one to two frames after Play Mode entry. The stats bar polls every editor update tick. Ensure cameras and audio sources are active in the scene before entering Play Mode.

---

## Profiler Flags Every Frame as Slow

**Symptom:** All frames in the Profiler tab are flagged slow regardless of actual FPS.

**Cause:** `SlowFrameThresholdMS` is set below the target frame time.

**Fix:** Open `Edit > Project Settings > Runtime Atlas` and increase `SlowFrameThresholdMS`. Default is `33.3 ms` (30 FPS target). For 60 FPS, use `16.7 ms`. For 120 FPS, use `8.3 ms`.

---

## Report Export Fails or Produces an Empty File

**Symptom:** Clicking **Export** produces no file, an empty file, or logs an error.

**Fixes:**

1. Click **Generate Preview** before clicking **Export**. Export operates on the preview snapshot, not live data.
2. Choose a writable destination directory. Avoid `Program Files`, system-protected paths, or paths containing non-ASCII characters on Windows.
3. Check the Unity Console for the specific IO error message.

---

## Mixer Tab Shows No Parameters

**Symptom:** The Mixer tab is empty or shows a prompt to configure a mixer.

**Cause:** No `AudioMixer` with exposed parameters has been configured.

**Fix:** Run the auto-config utility:

```
Window > Runtime Atlas > Auto-Config Audio Mixer
```

Or configure a mixer manually. See [Audio Mixer Setup](guides/audio-mixer-setup.md).

---

## Build Fails with Runtime Atlas Editor Types

**Symptom:** Player build fails with errors referencing `RuntimeAtlas.Editor` types.

**Cause:** A custom `.asmdef` in the project incorrectly references `RuntimeAtlas.Editor`, which is Editor-only.

**Fix:**

1. Locate every `.asmdef` in your project that references `RuntimeAtlas.Editor`.
2. Ensure those assemblies have **Editor** listed under **Platforms** (Editor only), or remove the reference if it is not needed.
3. Editor-only assemblies must only be referenced by other Editor-only assemblies.

---

## First-Run Dialog Appears on Every Launch

**Symptom:** The `Runtime Atlas installed` dialog appears on every Unity startup.

**Cause:** The `RuntimeAtlas.Upgrade.1.0.0.EditorUX` EditorPrefs key is being reset or is not persisting.

**Fix:** If `UserSettings/EditorUserSettings.asset` is excluded from version control for your user, the EditorPrefs key will not persist across sessions. Ensure that file is not forcibly cleared by your VCS setup.

---

## Input Does Not Work in Demo Scene

**Symptom:** Pressing `H` or `T` in the demo scene has no effect.

**Causes and fixes:**

| Cause | Fix |
|-------|-----|
| Game view does not have focus | Click the Game view to focus it before pressing keys |
| Legacy Input Manager not configured | Set `Project Settings > Player > Active Input Handling` to `Input Manager (Old)` or `Both` |
| New Input System not installed | Install `com.unity.inputsystem` via Package Manager |

`RADemoInputCompat` checks the Input System first (via reflection) and falls back to legacy input. Either backend works; neither needs to be installed exclusively.

---

## Getting Further Help

- [Discord](https://discord.gg/g5sNBZHZBd) — `#runtime-atlas` channel
- Purchase or licensing issues: contact support through the platform you purchased from
