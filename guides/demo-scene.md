# Demo Scene

**Runtime Atlas v1.1.0**

---

## Overview

Runtime Atlas ships with a pre-built demo scene designed to populate every diagnostic tab with real data immediately on Play Mode entry. It is an optional component — the demo scene is not required to use Runtime Atlas in your own project.

---

## Location

```
Assets/RuntimeAtlas/Demo/Scene/RA.unity
```

Open via the **Project** window or double-click to set as the active scene.

---

## Building the Scene

To rebuild the demo scene from scratch at any time:

```
Window > Runtime Atlas > Build Demo Scene
```

This runs `RADemoSceneBuilder` and generates the full scene hierarchy programmatically. Any manual changes to the existing demo scene will be replaced.

---

## Scene Contents

### Cameras (3)

| Object | Component | Purpose |
|--------|-----------|---------|
| `MainCamera` | `Camera` | Primary perspective camera (FOV 60, depth 0) |
| `SecurityCamera` | `Camera` | Secondary camera for multi-camera alert testing (depth 0, triggers equal-depth warning) |
| `MiniMapCamera` | `Camera` | Orthographic overhead camera (depth -2) |

Three cameras are present to generate Camera tab data and demonstrate alert conditions (equal depth on Main and Security Camera triggers a warning).

### Audio Sources (3)

| Object | Purpose |
|--------|---------|
| `BGM_Source` | Background music source. Assigned to Music mixer group. |
| `Ambient_Source` | Ambient sound source. Assigned to Ambient mixer group. |
| `SFX_Source` | Sound effects source. Assigned to SFX mixer group. |

An `AudioListener` is on the `MainCamera`.

### Physics Objects

| Object | Component | Purpose |
|--------|-----------|---------|
| `Platform_0` through `Platform_2` | `RADemoKinematicMover` | Kinematic rigidbody platforms oscillating vertically |
| `PhysCube_0` through `PhysCube_4` | `Rigidbody` | Dynamic physics cubes resting on platforms |
| `MatSphere_0` through `MatSphere_4` | `Renderer` | Static spheres with distinct materials for Materials tab |

### Demo Controllers

| Object | Component | Purpose |
|--------|-----------|---------|
| `=== Runtime Atlas Demo ===` (root) | `RADemoController` | On-screen HUD and keyboard shortcuts |
| `=== Runtime Atlas Demo ===` (root) | `RADemoStressTester` | Configurable GC and physics stress generator |

### Environment

| Object | Purpose |
|--------|---------|
| `Floor`, `Wall_Back`, `Wall_Left`, `Wall_Right` | Static geometry providing physics collision surfaces |
| `Directional Light` | Scene lighting |

---

## Stress Tester Configuration

The `RADemoStressTester` component on the root object controls load generation. Its fields are set via the Unity Inspector.

| Field | Default | Effect |
|-------|---------|--------|
| `gcAllocBytesPerFrame` | `0` | Set to a non-zero value to allocate heap each frame |
| `spawnPhysicsObjects` | `false` | Enable to spawn rigidbodies at runtime |
| `maxSpawnedObjects` | `20` | Cap on concurrently spawned objects |
| `startInStressMode` | `false` | Start in stress mode without pressing T |
| `stressToggleKey` | `T` | Key to toggle stress mode at runtime |

---

## Runtime Keys

| Key | Action |
|-----|--------|
| `H` | Toggle the on-screen HUD |
| `T` | Toggle stress mode |

---

## Expected Tab Data

| Tab | What the demo populates |
|-----|------------------------|
| Camera | 3 cameras with distinct properties; equal-depth warning between Main and Security |
| Audio | 3 audio sources + listener |
| Alerts | At least one camera depth warning; additional alerts if stress mode is active |
| Profiler | Live frame data from the running scene |
| Graph | Camera, audio, and alert nodes connected |
| Physics | 3 kinematic rigidbodies + 5 dynamic cubes |
| Materials | 5 material spheres + environment meshes |
| Timeline | Circular buffer filling with per-frame snapshots |
| Console | No output unless `[RA]`-tagged `Debug.Log` calls are added |

---

## Notes

- The demo scene uses `GameObjects` named with the `=== Runtime Atlas Demo ===` convention for easy identification in the Hierarchy.
- Spawned physics objects from `RADemoStressTester` are created and destroyed at runtime. They are not saved to the scene.
- All spawned rigidbodies and their materials are cleaned up in `OnDestroy` — no asset leaks on Play Mode exit.
