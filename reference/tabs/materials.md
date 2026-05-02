# Materials Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Provides an overview of materials and shaders used by `Renderer` components in the active scene. Helps identify material count, shader distribution, and instanced material issues.

---

## Scene Statistics

| Statistic | Description |
|-----------|-------------|
| **Total materials** | Unique material assets used across all renderers |
| **Total renderers** | `Renderer` components in the scene |
| **Unique shaders** | Distinct shaders across all materials |
| **Instance materials** | Materials instantiated at runtime (accessed via `Renderer.material` not `sharedMaterial`) |

---

## Material List

Each material entry:

| Field | Description |
|-------|-------------|
| **Name** | Material asset name |
| **Shader** | Assigned shader name |
| **Renderer count** | Number of renderers using this material |
| **Instanced** | Whether this material was instantiated (i.e., differs from `sharedMaterial`) |
| **Keywords** | Active shader keyword list |

---

## Shader Summary

Groups materials by shader:

| Field | Description |
|-------|-------------|
| **Shader name** | Full shader path (e.g., `Standard`, `Universal Render Pipeline/Lit`) |
| **Material count** | Materials using this shader |
| **Renderer count** | Total renderers affected |

---

## Instanced Material Detection

Materials accessed via `Renderer.material` (rather than `Renderer.sharedMaterial`) are instantiated by Unity and flagged as instanced. Each instance consumes separate GPU memory and breaks GPU instancing for those renderers. The Materials tab makes these visible.

---

## Refresh

Data is populated on tab activation. Click the tab again or press **Refresh** to re-poll. The tab does not update continuously.
