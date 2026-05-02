# Physics Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Displays scene-wide physics statistics and per-object `Rigidbody` state. Available in Play Mode and Edit Mode; data is more meaningful during Play Mode when physics is simulating.

---

## Scene Statistics

| Statistic | Description |
|-----------|-------------|
| **Dynamic rigidbodies** | Non-kinematic `Rigidbody` components in the scene |
| **Kinematic rigidbodies** | Kinematic `Rigidbody` components |
| **Static colliders** | `Collider` components with no `Rigidbody` parent |
| **Active joints** | `Joint` components present in the scene |
| **Fixed update interval** | `Time.fixedDeltaTime` in milliseconds |

---

## Per-Object Display

Each `Rigidbody` in the scene is listed with:

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Mass** | Rigidbody mass |
| **Velocity** | World-space linear velocity magnitude (m/s) |
| **Angular velocity** | World-space angular velocity magnitude (rad/s) |
| **Sleeping** | Whether the physics engine has sleeping this body |
| **Kinematic** | Kinematic enabled state |
| **Gravity** | Use gravity state |
| **Constraints** | Active position and rotation freeze axes |

---

## Notes

- The Physics tab reads data from the Unity physics engine each editor frame in Play Mode.
- It does not write to or modify physics state.
- The tab does not provide a collision matrix editor. The Unity collision matrix is read via `Physics.GetIgnoreLayerCollision` and displayed for reference.
