# Materials Tab

**Runtime Atlas v1.1.0**

---

## Purpose

Provides an overview of materials and shaders used by `Renderer` components in the active scene. Helps identify material count, shader distribution, and potential rendering configuration issues.

---

## Scene Material Statistics

| Statistic | Description |
|-----------|-------------|
| **Total materials** | Count of unique material assets used in the scene |
| **Total renderers** | Count of `Renderer` components in the scene |
| **Shaders used** | Count of unique shaders across all materials |
| **Instance materials** | Materials instantiated at runtime (`Renderer.material`, not `sharedMaterial`) |

---

## Material List

Each material is listed with:

| Field | Description |
|-------|-------------|
| **Name** | Material asset name |
| **Shader** | Assigned shader name |
| **Renderer count** | Number of renderers using this material |
| **Instanced** | Whether this material has been instantiated (not a shared asset) |
| **Keywords** | Active shader keyword list |

---

## Shader Summary

A secondary section groups materials by shader:

| Field | Description |
|-------|-------------|
| **Shader name** | Full shader path (e.g., `Standard`, `Universal Render Pipeline/Lit`) |
| **Material count** | Number of materials using this shader |
| **Renderer count** | Total renderers affected |

---

## Notes

- Instance material detection relies on Unity's `Renderer.sharedMaterial` vs `Renderer.material` comparison. Materials accessed via `Renderer.material` are flagged as instanced — each instance consumes separate memory and breaks GPU instancing for those renderers.
- The Materials tab reads data on tab activation. It does not update continuously. Click the tab again or press **Refresh** to re-poll.
