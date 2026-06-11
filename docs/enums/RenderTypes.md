Modelpart render types that can be applied via <code>setPrimaryRenderType(string)</code> or <code>setSecondaryRenderType(string)</code>

There can only be one primary and secondary type applied to a cube at once, so you may get unwanted behavior if you make the primary render type `LINES` as all the pixels aside from the lines will vanish.

**Example**:

```lua
models.myModel:setPrimaryRenderType("END_PORTAL")
models.myModel:setSecondaryRenderType("EMISSIVE")
```

---

## All Render Types

| Render Type             | Description |
| ----------------------- | ----------- |
| `NONE`                  | Invisible   |
| `CUTOUT`                | Standard    |
| `CUTOUT_CULL`           | Standard (No Inside Faces)           |
| `TRANSLUCENT`           | Standard           |
| `TRANSLUCENT_CULL`      | Standard (No Inside Faces)           |
| `EMISSIVE`              | Fully Lit (Transparent)           |
| `EMISSIVE_SOLID`        | Fully Lit (No Inside Faces)          |
| `CUTOUT_EMISSIVE_SOLID` | Fully Lit            |
| `EYES`                  | Fully Lit (Transparent)           |
| `END_PORTAL`            | No-perspective End Portal Texture           |
| `END_GATEWAY`           | No-perspective End Gateway Texture           |
| `TEXTURED_PORTAL`       | No-perspective Geometric Texture           |
| `GLINT`                 | -           |
| `GLINT2`                | -           |
| `TEXTURED_GLINT`        | -           |
| `LINES`                 | White Lines Around Edges ?          |
| `LINES_STRIP`           | White Lines Between Vertices ?           |
| `SOLID`                 | Fully Lit (No Texture, Only White)           |
| `BLURRY`                | Smoothed texture           |

Visual Flighthrough Example:

https://files.catbox.moe/anp21h.webm
