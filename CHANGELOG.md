# Runtime Atlas — Changelog

**Publisher:** Tools Studio | **Product:** Paid — [purchase here](https://assetstore.unity.com/packages/slug/367424)

This changelog covers the Runtime Atlas package. For documentation-only changes,
see commit history in this repository.

---


---

## Version 1.1.0

### Breaking Changes

- **Namespace migration.** All public types have moved:
  - `Arish.RA` → `RuntimeAtlas`
  - `Arish.RA.Editor` → `RuntimeAtlas.Editor`
  - Projects referencing `using Arish.RA;` or `using Arish.RA.Editor;` must update those directives.
  - Affected public types: `AlertEntry`, `AlertSeverity` (previously in `Arish.RA`).

### Added

- `IAlertSource` interface (`RuntimeAtlas.Editor`) — decouples alert producers from `AlertSystem`. Implement on any class to contribute alerts without direct coupling to inspector nodes.
- `RuntimeAtlas.Editor.Demo` assembly — isolates the `RADemoSceneBuilder` editor utility from the main editor assembly.
- `RuntimeAtlas.Tests` assembly — edit-mode test suite. Not included in Asset Store package exports.
- Individual MonoBehaviour source files for all demo scene behaviours (`RADemoKinematicMover`, `RADemoSpinner`, `RADemoBouncer`, `RADemoStressTester`, `RADemoController`).

### Fixed

- Demo scene missing-script warnings on `RADemoSpinner`, `RADemoStressTester`, and `RADemoController`. Root cause: incomplete `.meta` file for multi-class source file. All demo MonoBehaviours now have individual files with stable GUIDs.
- `ExecuteMenuItem("Component/Scripts")` console error when clicking the Add Component button in the Inspector tab. This menu path was removed in Unity 6. Fixed with a Unity 6-safe fallback.

### Changed

- `RuntimeAtlas.Editor` assembly no longer references `RuntimeAtlas.Core.Demo`. Demo-editor dependency is now isolated in `RuntimeAtlas.Editor.Demo`.
- `rootNamespace` of `RuntimeAtlas.Editor.asmdef` updated to `RuntimeAtlas.Editor`.
- All file header comments updated to reflect version 1.1.0.

---

## Version 1.0.0

### Added

- Runtime Atlas editor window with 18 diagnostic tabs: Camera, Audio, Graph, Timeline, Alerts, Profiler, Physics, Scanner, Optimizer, Scripts, Inspector, Animator, Mixer, Scene, Report, Console, Materials, About.
- Frame-accurate performance profiler recording FPS, frame time, GC alloc delta, draw calls, triangles, vertices, and SetPass calls.
- Alert system with severity levels (Info, Warning, Critical), aggregation by group key, and dismissal support.
- Runtime console with prefixed log capture (`[RA]`, `[Runtime Atlas]`, `[RuntimeAtlas]`), ring buffer storage, and text export.
- Timeline recorder capturing per-frame snapshots of camera, audio, alert count, FPS, and memory.
- Session report generator supporting JSON, HTML, Markdown, and CSV export formats.
- Script scanner detecting empty lifecycle methods, `FindObjectOfType` in hot paths, and missing null checks.
- Optimizer suggestions derived from scanner results with actionable fix descriptions.
- One-click demo scene builder (`Window > Runtime Atlas > Build Demo Scene`).
- Audio Mixer auto-config utility (`Window > Runtime Atlas > Auto-Config Audio Mixer`).
- Demo scene with kinematic platform, spinning objects, bouncing objects, stress tester, and HUD controller.
- Input System compatibility layer supporting both legacy Input Manager and the new Input System.
- Package bootstrap with first-run upgrade dialog.
