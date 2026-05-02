# Physics Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Displays all `Rigidbody` components and `Collider` components in the current scene, and shows the full physics layer collision matrix. Data is polled from the scene every 4 Hz in Play Mode; the layer matrix is read from `Physics.GetIgnoreLayerCollision`.

---

## Sub-tabs

| Sub-tab | Content |
|---------|---------|
| Bodies | All `Rigidbody` components with live velocity and state |
| Colliders | All `Collider` components with type, mode, and bounds |
| Layer Matrix | Full 32×32 physics layer collision matrix |

---

## Bodies Sub-tab

| Column | Description |
|--------|-------------|
| Name | GameObject name |
| Speed | `rigidbody.velocity.magnitude` in units/s |
| Velocity | Vector3 velocity (X, Y, Z) |
| Mass | `rigidbody.mass` |
| State | Kinematic / Dynamic / Sleeping |
| Layer | Physics layer name |
| CD Mode | `CollisionDetectionMode` (Discrete / Continuous / ContinuousDynamic / etc.) |

---

## Colliders Sub-tab

| Column | Description |
|--------|-------------|
| Name | GameObject name |
| Type | Box / Sphere / Capsule / Mesh / Terrain |
| Mode | Trigger or Collider |
| Layer | Physics layer name |
| Material | `PhysicMaterial` name, or "(none)" |
| Has RB | Whether the GameObject or a parent has a `Rigidbody` |
| Bounds | World-space bounds size (X, Y, Z) |

---

## Layer Matrix Sub-tab

Shows a 32×32 grid where each cell indicates whether two physics layers collide. Cells are colour-coded:

| Colour | Meaning |
|--------|---------|
| Green | Layers collide |
| Red | Layers do not collide (ignored) |
| Grey | Empty / unnamed layer |

The **Show Empty Layers** toggle includes unnamed layers in the matrix. By default they are hidden to reduce visual noise.

The matrix is read-only. To change collision settings, use **Edit > Project Settings > Physics**.
