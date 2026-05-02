# Runtime Atlas — Changelog

**Publisher:** Tools Studio

---

## Version 1.2.0

### Added

- Asset version header (`Asset : Runtime Atlas Version 1.2.0`) standardised across all 44 source files. Every `.cs` file now carries a complete, consistent header block including asset name, publisher, description, namespace, and assembly.

### Changed

- Version constant `k_Version` in `AtlasWindow` updated to `"Version 1.2.0"`.
- Version display string in `RASettingsProvider` updated to `"Version 1.2.0 | Tools Studio"`.

### Fixed

- `ScriptViewerWindow`: `GUIContent` for the script icon, **Open in IDE** button, and **Close** button were allocated on every `DrawGUI` call. All three are now cached with null-check and icon-refresh guards. Eliminates per-repaint GC allocation from this path.
- `ComponentInspectorPanel`: `GUIContent` for **Lock**, **Clear**, search icon, jump-to icon, and **Remove Component** were allocated on every repaint. All five are now cached.
- `AnimatorMonitor`: `GUIContent` for the search icon, refresh icon, and jump-to icon were allocated on every repaint. All three are now cached.
- `AudioMixerPanel`: `GUIContent` for the **Auto** button and rescan icon were allocated on every repaint. Both are now cached.
- `AtlasWindow.DrawActiveTabSafely`: a module that opened layout groups and then threw an exception would leave those groups open on the IMGUI stack. `OnGUI`'s `finally` block then called `EndScrollView`/`EndArea` against a partially-drained stack, producing `EndLayoutGroup: BeginLayoutGroup must be called first` and `InvalidOperationException: Stack empty`. Fixed by wrapping `DrawActiveTab()` in a `BeginVertical`/`EndVertical` buffer layer. On exception, the buffer is closed and `GUIUtility.ExitGUI()` is called to force a clean layout stack on the next repaint. The `finally` block now catches secondary stack errors independently so the primary log entry is never masked.
- `RADemoController`: `new Texture2D(1, 1)` was missing `hideFlags = HideFlags.HideAndDontSave`. Fixed to prevent texture leakage across domain reloads.

---

## Version 1.1.0

### Breaking Changes

- **Namespace migration.** All public types have moved:

| Previous namespace | New namespace |
|-------------------|--------------|
| `Arish.RA` | `RuntimeAtlas` |
| `Arish.RA.Editor` | `RuntimeAtlas.Editor` |

Affected public types: `AlertEntry`, `AlertSeverity`. All editor classes. See [Upgrade Guide](getting-started/upgrade-guide.md).

### Added

- `IAlertSource` interface (`RuntimeAtlas.Editor`) — decouples alert producers from `AlertSystem`. Implement on any class to contribute alerts without direct dependency on inspector node classes.
- `RuntimeAtlas.Editor.Demo` assembly — isolates `RADemoSceneBuilder` from the main editor assembly.
- `RuntimeAtlas.Tests` assembly — edit-mode test suite. Not included in Asset Store package exports.
- Individual MonoBehaviour source files for all five demo scene behaviours: `RADemoKinematicMover`, `RADemoSpinner`, `RADemoBouncer`, `RADemoStressTester`, `RADemoController`.

### Fixed

- Demo scene missing-script warnings on `RADemoSpinner`, `RADemoStressTester`, and `RADemoController`. Root cause: incomplete `.meta` for a multi-class source file. All demo MonoBehaviours now have individual files with stable GUIDs.
- `ExecuteMenuItem("Component/Scripts")` console error on Add Component click in the Inspector tab. This menu path was removed in Unity 6. Replaced with a Unity 6-safe fallback.

### Changed

- `RuntimeAtlas.Editor` assembly no longer references `RuntimeAtlas.Core.Demo`. Demo-editor dependency now isolated in `RuntimeAtlas.Editor.Demo`.
- `rootNamespace` of `RuntimeAtlas.Editor.asmdef` updated from `Arish.RA.Editor` to `RuntimeAtlas.Editor`.

---

## Version 1.0.0

### Added

- Runtime Atlas editor window with 18 diagnostic tabs: Camera, Audio, Graph, Timeline, Alerts, Profiler, Physics, Scanner, Optimizer, Scripts, Inspector, Animator, Mixer, Scene, Report, Console, Materials, About.
- Frame-accurate performance profiler recording FPS, frame time, GC allocation delta, draw calls, triangles, vertices, and SetPass calls.
- Alert system with severity levels (Info, Warning, Critical), aggregation by group key, and per-entry dismissal.
- Runtime console with prefixed log capture (`[RA]`, `[Runtime Atlas]`, `[RuntimeAtlas]`), fixed ring buffer, and plain-text export.
- Timeline recorder capturing per-frame cross-system snapshots with post-session scrub playback.
- Session report generator supporting JSON, HTML, Markdown, CSV, and DOCX export formats.
- Script scanner detecting empty lifecycle methods, `FindObjectOfType` in hot paths, and missing null checks.
- Optimizer suggestions derived from scanner results with fix descriptions.
- One-click demo scene builder (`Window > Runtime Atlas > Build Demo Scene`).
- Audio Mixer auto-config utility (`Window > Runtime Atlas > Auto-Config Audio Mixer`).
- Demo scene with kinematic platform, spinning objects, bouncing objects, stress tester, and HUD controller.
- Input System compatibility layer supporting legacy Input Manager and the new Input System.
- Package bootstrap with first-run dialog.
