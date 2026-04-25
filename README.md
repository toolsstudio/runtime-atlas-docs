# Runtime Atlas — Documentation

**Version:** 1.1.0 | **Publisher:** Tools Studio | **Unity:** 2021.3 LTS – 6.x

Runtime Atlas is a **paid** Unity Editor diagnostic toolkit. It provides live inspection,
performance profiling, alerting, and session reporting inside a single dockable editor window.

> **This repository contains documentation only.**
> Source code is not included and is not publicly available.
> The Runtime Atlas software is a commercial product — see [Purchase](#purchase) below.

---

## Purchase

Runtime Atlas is available on the following platforms:

- [Unity Asset Store](https://assetstore.unity.com/packages/slug/367424)
- [itch.io](https://tools-studio.itch.io/runtime-atlas-unity-debugging-performance-toolkit)
- [Gumroad](https://toolsstudio.gumroad.com/l/runtime-atlas)

Each platform delivers the same package. Purchase on whichever platform you prefer.

---

## Support

For questions, bug reports, and feature requests:

- [Discord](https://discord.gg/g5sNBZHZBd)
- For import and licensing issues, contact support via the platform you purchased from.

---

## Documentation

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
| [License](LICENSE.md) | Documentation license and software license notice |

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

---

## Related Tools

### MetaGuard

[MetaGuard](https://github.com/Afterix-Hub/MetaGuard) is a free, separate tool
from Tools Studio that addresses Unity GUID integrity. It is not bundled with
Runtime Atlas and has no dependency on it.

**What it does:**

MetaGuard scans a Unity project's `.meta` files to detect GUID integrity issues —
GUID collisions, zero GUIDs, malformed GUIDs, orphaned `.meta` files, missing
`.meta` files, broken asset references, and cyclic dependencies. Detected issues
are classified by risk level (Critical / High / Medium / Low) and reported with a
project health score. Before modifying anything, MetaGuard simulates every
proposed fix against a live dependency graph and assigns a verdict (Safe /
Warning / Dangerous / Destructive). Apply writes only approved operations,
protected by a pre-apply snapshot with 48-hour rollback.

**When it is relevant:**

- After merging branches that touched asset directories
- After bulk directory restructuring
- When Unity reports missing script or missing asset references with no obvious cause
- Before an Asset Store submission, to verify GUID cleanliness
- During project recovery after file-system-level moves or renames outside the Unity Editor

**Relationship to Runtime Atlas:**

The two tools address different problem classes. Runtime Atlas monitors runtime
behaviour — frame performance, audio state, camera configuration, alerts, and
diagnostics during Play Mode. MetaGuard operates entirely outside Play Mode on
the project's file-system layer. They do not overlap in function and can be used
independently or together.

**Links:**
- [MetaGuard](https://github.com/Afterix-Hub/MetaGuard) (source and download)
- [MetaGuard documentation](https://github.com/toolsstudio/metaguard-docs)

---

## Repository Notice

This repository contains documentation only. No source code, compiled assemblies,
or Unity package assets are present or will be added. The Runtime Atlas software
is governed by a separate commercial license — see [LICENSE.md](LICENSE.md).
