# Keyboard Shortcuts

**Runtime Atlas v1.2.0**

---

## Window

| Action | Menu path | Shortcut |
|--------|-----------|----------|
| Open Runtime Atlas | `Window > Runtime Atlas > Open` | `Ctrl+Alt+R` |

---

## Tab Navigation

Each entry opens the Runtime Atlas window and navigates directly to the specified tab.

| Tab | Menu path |
|-----|-----------|
| Inspector | `Window > Runtime Atlas > Tabs > Inspector` |
| Audio | `Window > Runtime Atlas > Tabs > Audio` |
| Animator | `Window > Runtime Atlas > Tabs > Animator` |
| Mixer | `Window > Runtime Atlas > Tabs > Mixer` |
| Console | `Window > Runtime Atlas > Tabs > Console` |

All tab shortcuts appear under `Window > Runtime Atlas > Tabs`. No additional keyboard shortcuts are assigned to individual tabs by default.

---

## Utilities

| Action | Menu path |
|--------|-----------|
| Build Demo Scene | `Window > Runtime Atlas > Build Demo Scene` |
| Auto-Config Audio Mixer | `Window > Runtime Atlas > Auto-Config Audio Mixer` |

---

## Demo Scene Runtime Keys

Active only when the demo scene is running in Play Mode. The Game view must have focus.

| Key | Action |
|-----|--------|
| `H` | Toggle the on-screen HUD |
| `T` | Toggle stress mode on `RADemoStressTester` |

The stress mode key can be changed via the `stressToggleKey` field on the `RADemoStressTester` component in the Inspector.

---

## Programmatic Tab Selection

Tabs can be selected from code:

```csharp
using RuntimeAtlas.Editor;
using UnityEditor;

// Get or open the window, then select a tab by name (case-insensitive).
AtlasWindow win = EditorWindow.GetWindow<AtlasWindow>();
win.SelectTab("Inspector");  // returns bool — false if name not found
```

Valid tab names: `Camera`, `Audio`, `Graph`, `Timeline`, `Alerts`, `Profiler`, `Physics`, `Scanner`, `Optimizer`, `Scripts`, `Inspector`, `Animator`, `Mixer`, `Scene`, `Report`, `Console`, `Materials`, `About`.
