# Demo Behaviours API
**Runtime Atlas v1.2.0**

---

## Assembly

`RuntimeAtlas.Core.Demo` | Namespace: `RuntimeAtlas`

These MonoBehaviours are included for the demo scene only. They are not intended for use in production projects. They ship in player builds only when the demo assembly is included in a build (it is excluded by default).

---

## RADemoController

```csharp
public sealed class RADemoController : MonoBehaviour
```

Coordinates all demo behaviours from a single component. Provides a Unity Inspector toggle panel to enable/disable individual demo systems at runtime.

**Serialized fields:**

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `enableStressTester` | `bool` | `true` | Enables/disables `RADemoStressTester` |
| `enableSpinner` | `bool` | `true` | Enables/disables `RADemoSpinner` |
| `enableBouncer` | `bool` | `true` | Enables/disables `RADemoBouncer` |
| `enableMover` | `bool` | `true` | Enables/disables `RADemoKinematicMover` |

---

## RADemoKinematicMover

```csharp
public sealed class RADemoKinematicMover : MonoBehaviour
```

Moves a `Rigidbody` kinematically along a configurable path.

**Serialized fields:**

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `speed` | `float` | `2.0f` | Movement speed (units/s) |
| `range` | `float` | `5.0f` | Movement range in each axis |
| `axis` | `Vector3` | `Vector3.right` | Movement axis |

---

## RADemoSpinner

```csharp
public sealed class RADemoSpinner : MonoBehaviour
```

Rotates the GameObject at a fixed angular velocity.

**Serialized fields:**

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `degreesPerSecond` | `float` | `90.0f` | Rotation speed |
| `axis` | `Vector3` | `Vector3.up` | Rotation axis (local space) |

---

## RADemoBouncer

```csharp
public sealed class RADemoBouncer : MonoBehaviour
```

Applies a periodic upward force to a `Rigidbody`, producing a bouncing motion.

**Serialized fields:**

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `forceMagnitude` | `float` | `5.0f` | Applied force magnitude |
| `interval` | `float` | `1.5f` | Seconds between force applications |

---

## RADemoStressTester

```csharp
public sealed class RADemoStressTester : MonoBehaviour
```

Instantiates prefabs on a timer to increase scene complexity and produce measurable performance data in the Profiler tab.

**Serialized fields:**

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `spawnPrefab` | `GameObject` | — | Prefab to instantiate |
| `spawnInterval` | `float` | `0.5f` | Seconds between spawns |
| `maxSpawnCount` | `int` | `50` | Maximum simultaneous spawned objects |
| `destroyOldest` | `bool` | `true` | Destroy oldest spawned object when limit reached |

---

## RADemoInputCompat

```csharp
public sealed class RADemoInputCompat : MonoBehaviour
```

Input compatibility layer. Conditionally uses the new Input System or legacy Input Manager depending on which packages are present in the project.

This component is required by the demo scene. It has no public API surface for external use.
