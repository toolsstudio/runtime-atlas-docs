# Changelog
**Runtime Atlas** | Publisher: Tools Studio

All notable changes are documented here.
Format: [Version] — Added / Changed / Fixed / Breaking

---

## 1.2.0 — Production Polish Release

**Release type:** Minor — stabilization pass. No new features, no API changes, no breaking changes.

### Fixed

- `RAStyles.MakeTex()`: `Texture2D` objects now carry `HideFlags.HideAndDontSave`, preventing unexpected serialization or garbage collection across domain reloads.
- `RAStyles.ClearCache()`: nine `Texture2D` instances previously leaked on every assembly reload. All textures are now destroyed via `DestroyImmediate` before references are nulled.
- `CameraInspectorNode.DrawGUI()` (edit mode): `FindObjectsByType<Camera>` was called on every `OnGUI` frame. Result is now cached and refreshed at most once per second.
- `CameraInspectorNode.DrawGUI()` (play mode): `new List<Camera>()` was allocated on every `OnGUI` frame. Replaced with a reused pre-allocated list.
- `CameraInspectorNode.DrawAdvanced()`: Post-processing volume query (`FindObjectsByType(volType)`) was called on every `OnGUI` frame per open camera card. Result is now cached and refreshed at most once per second.
- `AudioInspectorNode.DrawEditModePreview()`: two `FindObjectsByType` calls (`AudioListener`, `AudioSource`) were called on every `OnGUI` frame in edit mode. Both are now cached and refreshed at most once per second.
- `AnimatorMonitor.DrawEditModeList()`: `FindObjectsByType<Animator>` was called on every `OnGUI` frame. Result is now cached and refreshed at most once per second.
- `PhysicsInspectorPanel.DrawBodyHeader()`: `new GUIStyle(GUI.skin.box) { background = MakeTex(...) }` was constructed on every `OnGUI` frame. Replaced with a lazy-initialized static `s_BodyHeaderStyle`.
- `PhysicsInspectorPanel.DrawColliders()`: same pattern as above for the collider column header. Replaced with `s_ColHeaderStyle`.
- `PhysicsInspectorPanel.DrawLayerMatrix()`: `new List<int>(32)` and `new GUIStyle(RAStyles.LabelMuted)` were allocated on every frame. Replaced with a persistent instance field and a lazy-initialized static style.
- `PhysicsInspectorPanel`: added `AssemblyReloadEvents.beforeAssemblyReload` and `[DidReloadScripts]` cleanup hooks to destroy static `GUIStyle` and cached `Texture2D` objects on domain reload.
- `AudioMixerPanel`: status label `GUIStyle` (`LabelBold` tinted green or red) was allocated on every repaint. Replaced with lazy-initialized statics.
- `AudioMixerPanel.DrawSetupStep()`: `new GUIStyle(RAStyles.LabelBold)` was allocated on every call (called up to 4× per frame when the setup panel is open). Replaced with lazy-initialized statics.
- `RAReportPanel.DrawGUI()`: `new GUIStyle(EditorStyles.textArea)` and `new GUIStyle(RAStyles.LabelBold)` were allocated on every repaint. Replaced with lazy-initialized instance fields.
- `ScriptScanner.ScanFile()`: four `Regex.IsMatch(string, string)` calls created a new `Regex` object on every scanned line. All four patterns are now compiled static fields.
- `ScriptScanner.DrawGUI()`: search filter comparison used `.ToLower().Contains()`, allocating two strings per result row per frame. Replaced with `IndexOf(OrdinalIgnoreCase)`.

### Changed

- All `.cs` file headers updated: `Runtime Atlas Version 1.1.0` → `Runtime Atlas Version 1.2.0`.
- `AtlasWindow.k_Version` updated to `"Version 1.2.0"`.
- `RASettingsProvider` version display label updated to `"Version 1.2.0 | Tools Studio"`.

---

## 1.1.0

### Breaking Changes

**Namespace migration.** All public types moved from `Arish.RA` / `Arish.RA.Editor` to `RuntimeAtlas` / `RuntimeAtlas.Editor`. See the [Upgrade Guide](getting-started/upgrade-guide.md) for migration steps.

### Added

- `IAlertSource` interface (`RuntimeAtlas.Editor`) — decouples alert-producing modules from `AlertSystem`. Implement on custom inspector nodes to contribute alerts.
- `RuntimeAtlas.Editor.Demo.asmdef` — isolates `RADemoSceneBuilder` from the main editor assembly.
- `RuntimeAtlas.Tests.asmdef` — edit-mode test assembly. Excluded from package export.
- Individual MonoBehaviour files for all demo behaviours: `RADemoKinematicMover`, `RADemoSpinner`, `RADemoBouncer`, `RADemoStressTester`, `RADemoController`. Resolves missing-script warnings caused by the previous multi-class source file.
- ADR documents: `ADR-001-namespace-strategy.md`, `ADR-002-editor-runtime-split.md`.
- `ARCHITECTURE.md` at project root.

### Changed

- `RuntimeAtlas.Editor` assembly no longer references `RuntimeAtlas.Core.Demo` directly — dependency isolated in `RuntimeAtlas.Editor.Demo`.
- `ComponentInspectorPanel` Add Component button: replaced `ExecuteMenuItem("Component/Scripts")` (removed in Unity 6) with a Unity 6-safe fallback.
- `rootNamespace` of `RuntimeAtlas.Editor.asmdef` updated from `Arish.RA.Editor` to `RuntimeAtlas.Editor`.

### Fixed

- Demo scene missing-script warnings on `RADemoSpinner`, `RADemoStressTester`, `RADemoController`.
- Console error on Add Component button click in Unity 6.
- Material inspector header texture sharing.
- Animator parameter write spam during repaint.
- Screenshot capture RenderTexture and Texture2D lifecycle cleanup.
- Timeline graph line rendering using `Handles.BeginGUI/EndGUI`.
- Script viewer virtualized line drawing path.

---

## 1.0.0

### Added

- Initial release. 18-tab editor window: Camera, Audio, Graph, Timeline, Alerts, Profiler, Physics, Scanner, Optimizer, Scripts, Inspector, Animator, Mixer, Scene, Report, Console, Materials, About.
- Report generation and export: HTML, JSON, Markdown, CSV, DOCX.
- Demo scene and runtime demo behaviours.
- Alert pipeline with grouped presentation and severity filtering.
