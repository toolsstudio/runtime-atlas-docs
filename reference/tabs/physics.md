# Physics Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Displays scene-wide physics statistics and per-object Rigidbody state during Play Mode.

---

## Scene Statistics

| Statistic | Description |
|-----------|-------------|
| **Dynamic rigidbodies** | Count of non-kinematic `Rigidbody` components |
| **Kinematic rigidbodies** | Count of kinematic `Rigidbody` components |
| **Static colliders** | Count of colliders without a `Rigidbody` parent |
| **Active joints** | Count of `Joint` components |
| **Physics update time** | Reported fixed update interval (`Time.fixedDeltaTime`) |

---

## Per-Object Display

Each Rigidbody in the scene is listed with:

| Field | Description |
|-------|-------------|
| **Name** | GameObject name |
| **Mass** | Rigidbody mass |
| **Velocity** | World-space linear velocity magnitude |
| **Angular velocity** | World-space angular velocity magnitude |
| **Sleeping** | Whether the physics engine has put this body to sleep |
| **Kinematic** | Kinematic state |
| **Gravity** | Gravity enabled state |
| **Constraints** | Active position and rotation freeze constraints |

---

## Notes

The Physics tab reads data from Unity's physics engine each editor frame in Play Mode. It does not modify physics state. Changes must be made through the scene or Inspector.
