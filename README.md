# Runtime Atlas — Documentation

**Version:** 1.2.0 | **Publisher:** Tools Studio | **Unity:** 2021.3 LTS – 6.x

Runtime Atlas is a paid Unity Editor diagnostic toolkit. It provides live inspection of runtime systems, performance profiling, alert aggregation, script scanning, and session report export inside a single dockable editor window.

> This repository contains documentation only. Source code is not included.

---

## Purchase

| Platform | Link |
|----------|------|
| Unity Asset Store | [Unity Asset Store](https://assetstore.unity.com/packages/slug/367424) |
| itch.io | [itch.io](https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit) |
| Gumroad | [Gumroad](https://toolsstudio.gumroad.com/l/runtime-atlas) |

---

## Open the Window

```
Window > Runtime Atlas > Open    (Ctrl+Alt+R)
```

---

## Documentation Index

### Getting Started

| Document | Purpose |
|----------|---------|
| [Installation](getting-started/installation.md) | Requirements, import steps, validation checklist |
| [Quick Start](getting-started/quick-start.md) | First session in under five minutes |
| [Upgrade Guide](getting-started/upgrade-guide.md) | Migrating from earlier versions |

### Reference

| Document | Purpose |
|----------|---------|
| [Window Overview](reference/window-overview.md) | Header, tab rows, stats bar anatomy |
| [Settings Reference](reference/settings.md) | All Project Settings fields and defaults |
| [Tab Reference](reference/tabs/README.md) | Per-tab documentation for all 18 tabs |
| [Keyboard Shortcuts](reference/keyboard-shortcuts.md) | All menu paths and shortcut keys |

### Architecture

| Document | Purpose |
|----------|---------|
| [Architecture Overview](architecture/overview.md) | Assembly layout, module map, data flow |

### API Reference

| Document | Purpose |
|----------|---------|
| [Alert System](api/alert-system.md) | `IAlertSource`, `AlertSystem`, `AlertEntry`, `AlertSeverity` |
| [Performance Profiler](api/performance-profiler.md) | `PerfSample`, thresholds, profiler lifecycle |
| [Timeline Recorder](api/timeline-recorder.md) | `FrameData`, circular buffer, recording lifecycle |
| [Console Capture](api/console-capture.md) | `LogEntry`, ring buffer, tag filtering, export |
| [Report Generator](api/report-generator.md) | `ReportData`, export structs, format methods |
| [Demo Behaviours](api/demo-behaviours.md) | Runtime demo MonoBehaviours and input helper |

### Guides

| Document | Purpose |
|----------|---------|
| [Custom Alert Source](guides/custom-alert-source.md) | Implementing `IAlertSource` |
| [Report Export](guides/report-export.md) | Format reference and field mapping |
| [Audio Mixer Setup](guides/audio-mixer-setup.md) | Auto-config and manual mixer configuration |
| [Demo Scene](guides/demo-scene.md) | Contents, expected tab data, stress tester |

### Other

| Document | Purpose |
|----------|---------|
| [Troubleshooting](troubleshooting.md) | Common issues and fixes |
| [Changelog](CHANGELOG.md) | Version history |
| [Support](SUPPORT.md) | Support channels and reporting guidance |
| [License](LICENSE.md) | Software license notice |

---

## Assembly Summary

| Assembly | Namespace | Included in player build |
|----------|-----------|--------------------------|
| `RuntimeAtlas.Core` | `RuntimeAtlas` | Yes |
| `RuntimeAtlas.Core.Demo` | `RuntimeAtlas` | Yes (demo only) |
| `RuntimeAtlas.Editor` | `RuntimeAtlas.Editor` | No |
| `RuntimeAtlas.Editor.Demo` | `RuntimeAtlas.Editor` | No |
| `RuntimeAtlas.Tests` | `RuntimeAtlas.Tests` | No (excluded from package) |

---

## Related Tools

[MetaGuard](https://github.com/Afterix-Hub/MetaGuard) is a free, separate tool from Tools Studio that addresses Unity GUID integrity. It detects GUID collisions, orphaned `.meta` files, broken asset references, and related issues, with simulation-gated fixes and 48-hour rollback. It operates entirely outside Play Mode on the project's file-system layer and has no functional overlap with Runtime Atlas.
