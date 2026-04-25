# Troubleshooting

**Runtime Atlas v1.1.0**

---

## Compile Errors on Import

**Symptom:** Unity Console shows compile errors immediately after importing the package.

**Causes and fixes:**

| Cause | Fix |
|-------|-----|
| Namespace conflict with existing code using `Arish.RA` | Replace `using Arish.RA;` and `using Arish.RA.Editor;` with `using RuntimeAtlas;` and `using RuntimeAtlas.Editor;`. See the [Upgrade Guide](getting-started/upgrade-guide.md). |
| Duplicate assembly definition | Remove any existing `RuntimeAtlas.Core.asmdef` or `RuntimeAtlas.Editor.asmdef` from a prior incomplete import before re-importing. |
| Unity version below minimum | Runtime Atlas requires Unity 2021.3 LTS or later. |

---

## Window Does Not Appear

**Symptom:** `Window > Runtime Atlas` menu is missing, or clicking **Open** does nothing.

**Fixes:**

1. Confirm the import completed without compile errors. Errors prevent `[MenuItem]` attributes from registering.
2. Force a script recompile: **Assets > Reimport All** or delete the `Library/` folder and reopen the project.
3. Confirm `RuntimeAtlas.Editor.asmdef` exists at `Assets/RuntimeAtlas/Editor/RuntimeAtlas.Editor.asmdef`.

---

## "The referenced script (Unknown) is missing" in Demo Scene

**Symptom:** Yellow warning triangles on demo scene GameObjects, "The referenced script (Unknown) is missing" in the Console.

**Cause:** This warning occurred in v1.0.0 due to an incomplete `.meta` file for the multi-class demo behaviour file.

**Fix:** This is resolved in v1.1.0. Ensure you are running the v1.1.0 package. If upgrading from v1.0.0, delete `Assets/RuntimeAtlas` fully before re-importing. Do not merge the old and new packages.

---

## ExecuteMenuItem Console Error

**Symptom:** Console shows `ExecuteMenuItem target for Scripts does not exist` when clicking the **+ Add Component** button in the Inspector tab.

**Cause:** This error occurred in v1.0.0 when running on Unity 6. The `Component/Scripts` menu path was removed in Unity 6.

**Fix:** This is resolved in v1.1.0. The Add Component button now uses a Unity 6-safe code path. Upgrade to v1.1.0.

---

## Runtime Atlas Console Shows No Messages

**Symptom:** The Console tab shows "No messages captured yet" even during active Play Mode.

**Explanation:** This is expected behaviour. The Runtime Atlas Console only captures messages that start with `[RA]`, `[Runtime Atlas]`, or `[RuntimeAtlas]`. It does not capture all Unity log output.

To emit a message that appears here:

```csharp
Debug.Log("[RA] My diagnostic message");
```

The Unity Console (bottom of the Editor) continues to show all messages from all sources regardless of the Runtime Atlas Console state.

---

## Stats Bar Shows Zero Cameras or Sources

**Symptom:** The stats bar shows `Cameras: 0` or `Sources: 0` during Play Mode.

**Cause:** Runtime Atlas scans for active scene components. If cameras or sources are instantiated via prefab or are inactive at the time of the scan, they may not be counted on the first frame.

**Fix:** Ensure cameras and audio sources are active before entering Play Mode, or wait one to two frames after Play Mode entry for the scan to complete. The stats bar updates every editor frame.

---

## Profiler Shows All Frames as Slow

**Symptom:** Every frame in the Profiler tab is flagged as slow, even at high FPS.

**Cause:** The slow-frame threshold is set too low for your target frame rate.

**Fix:** Open the Profiler settings panel (⚙ in the window header) and increase the `SlowFrameThresholdMS` value. Default is `33.3 ms` (30 FPS target). For a 60 FPS target, set it to `16.7 ms`. For a 120 FPS target, set it to `8.3 ms`.

---

## Report Export Fails or Produces Empty File

**Symptom:** Clicking **Export** produces no file, produces an empty file, or shows an error.

**Cause:** The destination path is not writable, or **Generate Preview** was not clicked before export.

**Fix:**

1. Click **Generate Preview** before clicking **Export**.
2. Choose a destination directory that is writable (avoid `Program Files`, system-protected directories, or paths with non-ASCII characters on Windows).
3. Check the Unity Console for the specific IO error message.

---

## Mixer Tab Shows No Parameters

**Symptom:** The Mixer tab is empty or prompts to configure a mixer.

**Cause:** No `AudioMixer` with exposed parameters has been assigned to the Runtime Atlas settings.

**Fix:** Run the auto-config utility:

```
Window > Runtime Atlas > Auto-Config Audio Mixer
```

Or configure a mixer manually. See [Audio Mixer Setup](guides/audio-mixer-setup.md).

---

## Build Fails When Runtime Atlas Is Imported

**Symptom:** Player build fails with errors referencing Runtime Atlas Editor types.

**Cause:** An `asmdef` in your project incorrectly references `RuntimeAtlas.Editor`, which is an Editor-only assembly. Including Editor-only code in a player build causes this failure.

**Fix:**

1. Check every `.asmdef` in your project that references `RuntimeAtlas.Editor`.
2. Ensure those assemblies have `Editor` listed under **Platforms** (Editor only), or remove the reference if it is not needed.
3. Runtime Atlas Editor assemblies contain `Editor` in their name. They must only be referenced by other Editor-only assemblies.

---

## Upgrade Dialog Appears on Every Launch

**Symptom:** The "Runtime Atlas installed" first-run dialog appears every time Unity opens.

**Cause:** The `RuntimeAtlas.Upgrade.1.0.0.EditorUX` EditorPrefs key is being reset or blocked.

**Fix:** Open **Edit > Preferences** and confirm the key can be written. If you are using a shared Unity project where `UserSettings/` is version-controlled and excluded for your user, the key may not be persisting. Exclude or gitignore `UserSettings/EditorUserSettings.asset` from shared version control.

---

## Input Does Not Work in Demo Scene

**Symptom:** Pressing `H` or `T` in the demo scene has no effect.

**Cause:** The demo scene uses `RADemoInputCompat`, which supports both legacy Input Manager and the Input System. If neither is correctly configured, input may not register.

**Fix:**

- If using the **legacy Input Manager**: confirm `Project Settings > Player > Active Input Handling` is set to `Input Manager (Old)` or `Both`.
- If using the **new Input System**: confirm the `com.unity.inputsystem` package is installed.
- Confirm the Game view has focus when pressing keys. Unity does not receive key input when another window is focused.

---

## Getting Further Help

If your issue is not listed here:

- **Discord:** https://discord.gg/g5sNBZHZBd — post in the `#runtime-atlas` channel
- For purchase or licensing issues, contact support through the platform you purchased from:
  - Unity Asset Store: via the Asset Store review/support system
  - itch.io: via the itch.io purchase page
  - Gumroad: via the Gumroad purchase receipt
