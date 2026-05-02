# Materials Tab
**Runtime Atlas v1.2.0**

---

## Purpose

Lists all `Renderer` components in the scene with their assigned materials and shader information. Provides a searchable overview of the scene's material usage.

---

## Data Collection

Material data is polled every 4 Hz to avoid scene traversal overhead. The cache holds up to 512 material descriptors (LRU eviction). Projects with more than 512 unique materials will experience eviction of oldest entries.

---

## Renderer List

Each row represents one `Renderer` in the scene:

| Column | Description |
|--------|-------------|
| GameObject | Renderer's GameObject name |
| Renderer type | MeshRenderer / SkinnedMeshRenderer / SpriteRenderer / etc. |
| Material name | Primary material name |
| Shader | Shader name |
| Shader keywords | Active shader keywords (comma-separated) |
| Texture count | Number of textures referenced by the material |

---

## Search

The search field filters by GameObject name, material name, or shader name.

---

## Material Detail Panel

Clicking a row expands a detail panel showing all material properties from the shader:

| Property type | Display |
|---------------|---------|
| Float | Value with label |
| Color | Colour swatch |
| Texture | Texture name and ping button |
| Vector | X / Y / Z / W values |

Properties are read-only in this view. To edit material properties, use the Unity Inspector.
