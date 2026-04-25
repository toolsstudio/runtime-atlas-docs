# Demo Behaviours API

**Namespace:** `RuntimeAtlas`  
**Assembly:** `RuntimeAtlas.Core.Demo`  
**Runtime Atlas v1.1.0**

---

## Overview

The demo scene includes five MonoBehaviour components and one static utility class. All are contained in the `RuntimeAtlas.Core.Demo` assembly and ship as part of the package. They are used exclusively by the demo scene and serve as load-generation tools for testing Runtime Atlas diagnostics.

These types are not intended as production game components.

---

## `RADemoKinematicMover`

Moves a kinematic `Rigidbody` platform up and down using `Rigidbody.MovePosition` on `FixedUpdate`.

### Inspector Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `Amplitude` | `float` | `2.5` | Peak displacement in metres |
| `Frequency` | `float` | `0.4` | Oscillation cycles per second |

### Requirements

Requires a `Rigidbody` component on the same GameObject with `isKinematic = true`.

---

## `RADemoSpinner`

Rotates the Transform around a configurable axis each `Update`.

### Inspector Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `DegreesPerSecond` | `float` | `45` | Rotation speed |
| `Axis` | `Vector3` | `Vector3.up` | Rotation axis in local space |

---

## `RADemoBouncer`

Applies a sine-wave vertical offset to the Transform's Y position each `Update`.

### Inspector Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `Height` | `float` | `2.5` | Peak bounce height in metres |
| `Speed` | `float` | `1.8` | Bounce frequency multiplier |

---

## `RADemoStressTester`

Applies configurable GC pressure and optional physics spawning during Play Mode. Used to generate load for profiler and alert testing.

### Inspector Fields

| Section | Field | Type | Default | Description |
|---------|-------|------|---------|-------------|
| GC Pressure | `gcAllocBytesPerFrame` | `int` | `0` | Bytes allocated per frame while stress mode is active. `0` disables GC stress. |
| Physics Spawner | `spawnPhysicsObjects` | `bool` | `false` | Spawn additional rigidbodies during stress mode |
| Physics Spawner | `maxSpawnedObjects` | `int` | `20` | Maximum concurrently spawned objects |
| Physics Spawner | `spawnInterval` | `float` | `1.5` | Seconds between spawns |
| Stress Control | `startInStressMode` | `bool` | `false` | Begin in stress mode when Play Mode starts |
| Stress Control | `allowRuntimeToggle` | `bool` | `true` | Allow toggling stress mode with a key at runtime |
| Stress Control | `stressToggleKey` | `KeyCode` | `KeyCode.T` | Key used to toggle stress mode |

### Runtime Property

| Property | Type | Description |
|----------|------|-------------|
| `IsHighStressMode` | `bool` | Read-only. Current stress mode state. |

---

## `RADemoController`

Master orchestrator for the demo scene. Renders an on-screen HUD during Play Mode showing active system status and keyboard shortcuts. Reads from `RADemoStressTester` for stress mode display.

### Inspector Fields

None. The controller auto-discovers the `RADemoStressTester` in the scene.

### Runtime Keyboard Controls

| Key | Action |
|-----|--------|
| `H` | Toggle HUD visibility |

---

## `RADemoInputCompat`

```csharp
public static class RADemoInputCompat
```

Static input compatibility helper. Supports both legacy `Input Manager` and the Unity `Input System` without requiring either as a hard dependency.

### Method

```csharp
// Returns true if the specified key was pressed this frame.
// Checks the Input System first (via reflection), then falls back to legacy Input.
public static bool GetKeyDown(KeyCode keyCode)
```

This class uses runtime reflection to detect the Input System. There is no compile-time dependency on `com.unity.inputsystem`.
