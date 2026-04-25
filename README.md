# Runtime Atlas — Documentation

**Version:** 1.1.0 | **Publisher:** Tools Studio | **Unity:** 2021.3 LTS – 6.x

Runtime Atlas is a Unity Editor diagnostic toolkit. It provides live inspection, performance profiling, alerting, and session reporting inside a single dockable editor window.

---

## Navigation

### Getting Started
| Document | Purpose |
|----------|---------|
| [Installation](getting-started/installation.md) | Requirements, import steps, validation checklist |
| [Quick Start](getting-started/quick-start.md) | First session in under five minutes |
| [Upgrade Guide](getting-started/upgrade-guide.md) | Migrating from v1.0.0 to v1.1.0 |

### Reference
| Document | Purpose |
|----------|---------|
| [Window Overview](reference/window-overview.md) | Anatomy of the Runtime Atlas window |
| [Tab Reference](reference/tabs/) | Per-tab documentation for all 18 tabs |
| [Keyboard Shortcuts](reference/keyboard-shortcuts.md) | All menu paths and shortcut keys |

### API Reference
| Document | Purpose |
|----------|---------|
| [Alert System](api/alert-system.md) | `IAlertSource`, `AlertSystem`, `AlertEntry`, `AlertSeverity` |
| [Performance Profiler](api/performance-profiler.md) | `PerfSample`, thresholds, profiler state |
| [Timeline Recorder](api/timeline-recorder.md) | `FrameData`, recording lifecycle |
| [Console Capture](api/console-capture.md) | `LogEntry`, filters, ring buffer, export |
| [Report Generator](api/report-generator.md) | `ReportData`, export formats |
| [Demo Behaviours](api/demo-behaviours.md) | Runtime demo MonoBehaviours |

### Guides
| Document | Purpose |
|----------|---------|
| [Custom Alert Source](guides/custom-alert-source.md) | Implementing `IAlertSource` |
| [Report Export](guides/report-export.md) | All export formats explained |
| [Audio Mixer Setup](guides/audio-mixer-setup.md) | Auto-configuring the Audio Mixer |
| [Demo Scene](guides/demo-scene.md) | Running and configuring the demo scene |

### Other
| Document | Purpose |
|----------|---------|
| [Troubleshooting](troubleshooting.md) | Common issues and resolutions |
| [Changelog](CHANGELOG.md) | Version history |

---

## Assemblies

| Assembly | Namespace | Ships in player build |
|----------|-----------|----------------------|
| `RuntimeAtlas.Core` | `RuntimeAtlas` | Yes |
| `RuntimeAtlas.Core.Demo` | `RuntimeAtlas` | Yes (demo only) |
| `RuntimeAtlas.Editor` | `RuntimeAtlas.Editor` | No |
| `RuntimeAtlas.Editor.Demo` | `RuntimeAtlas.Editor` | No |

---

## Open Runtime Atlas

```
Window > Runtime Atlas > Open    (Ctrl+Alt+R)
```
