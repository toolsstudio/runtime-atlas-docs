# Runtime Atlas — Documentation
**Version:** 1.2.0 | **Publisher:** Tools Studio | **Unity:** 2021.3 LTS – 6.x

Runtime Atlas is a paid Unity Editor diagnostic toolkit. It provides live camera, audio, physics, and performance inspection, a script quality scanner, alert aggregation, and multi-format session reporting — all inside a single dockable editor window.

> **This repository contains documentation only.**
> Source code is not included. Runtime Atlas is a commercial product.

---

## Purchase

| Platform | Link |
|----------|------|
| [Unity Asset Store](https://assetstore.unity.com/packages/slug/367424) |
| [itch.io Page](https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit) |
| [Gumroad Store](https://toolsstudio.gumroad.com/l/runtime-atlas) |

All platforms deliver the same package.

---

## Support

- **Discord:** [Join Discord](https://discord.gg/g5sNBZHZBd) — primary support channel (`#runtime-atlas`)
- **Platform support:** For purchase, refund, or licensing issues, use the support channel on the platform you purchased from.

See [SUPPORT.md](SUPPORT.md) for full contact guidance.

---

## Getting Started

| Document | Purpose |
|----------|---------|
| [Installation](getting-started/installation.md) | Requirements, import steps, validation checklist |
| [Quick Start](getting-started/quick-start.md) | First session in under five minutes |
| [Upgrade Guide](getting-started/upgrade-guide.md) | Migrating from previous versions |

---

## Reference

| Document | Purpose |
|----------|---------|
| [Window Overview](reference/window-overview.md) | Header bar, stats bar, tab layout |
| [Tab Reference](reference/tabs/) | Per-tab documentation for all 18 tabs |
| [Keyboard Shortcuts](reference/keyboard-shortcuts.md) | All menu paths and shortcut keys |

---

## API Reference

| Document | Purpose |
|----------|---------|
| [Alert System](api/alert-system.md) | `IAlertSource`, `AlertSystem`, `AlertEntry`, `AlertSeverity` |
| [Performance Profiler](api/performance-profiler.md) | `PerfSample`, thresholds, profiler lifecycle |
| [Timeline Recorder](api/timeline-recorder.md) | `FrameData`, recording lifecycle, ring buffer |
| [Console Capture](api/console-capture.md) | `LogEntry`, filters, ring buffer, prefix rules |
| [Report Generator](api/report-generator.md) | `ReportData`, formats, export path |
| [Demo Behaviours](api/demo-behaviours.md) | Runtime demo MonoBehaviours |

---

## Guides

| Document | Purpose |
|----------|---------|
| [Custom Alert Source](guides/custom-alert-source.md) | Implementing `IAlertSource` in your own code |
| [Report Export](guides/report-export.md) | All export formats with field reference |
| [Audio Mixer Setup](guides/audio-mixer-setup.md) | Auto-configuring the Audio Mixer panel |
| [Demo Scene](guides/demo-scene.md) | Running and rebuilding the demo scene |

---

## Other

| Document | Purpose |
|----------|---------|
| [Troubleshooting](troubleshooting.md) | Common issues and step-by-step resolutions |
| [Changelog](CHANGELOG.md) | Version history |
| [License](LICENSE.md) | Documentation license and software license notice |

---

## Assemblies

| Assembly | Namespace | Ships in player build |
|----------|-----------|----------------------|
| `RuntimeAtlas.Core` | `RuntimeAtlas` | Yes |
| `RuntimeAtlas.Core.Demo` | `RuntimeAtlas` | Yes (demo scenes only) |
| `RuntimeAtlas.Editor` | `RuntimeAtlas.Editor` | No |
| `RuntimeAtlas.Editor.Demo` | `RuntimeAtlas.Editor` | No |
| `RuntimeAtlas.Tests` | `RuntimeAtlas.Tests` | No (excluded from export) |

---

## Open the Window

```
Window > Runtime Atlas > Open    (Ctrl+Alt+R)
```

---

## Related Tools

**MetaGuard** is a free, separate tool from Tools Studio that addresses Unity `.meta` file and GUID integrity. It is not bundled with Runtime Atlas.

- Source and download: [MetaGuard on GitHub](https://github.com/Afterix-Hub/MetaGuard)
- Documentation: [MetaGuard Documentation](https://github.com/toolsstudio/metaguard-docs)

The two tools address different problem classes. Runtime Atlas monitors runtime behaviour during Play Mode. MetaGuard operates outside Play Mode on the project file-system layer. They do not overlap in function.
