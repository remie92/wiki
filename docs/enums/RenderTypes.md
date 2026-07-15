Modelpart render types that can be applied via <code>setPrimaryRenderType(string)</code> or <code>setSecondaryRenderType(string)</code>

There can only be one primary and secondary type applied to a cube at once, so you may get unwanted behavior if you make the primary render type `LINES` as all the pixels aside from the lines will vanish.

**Example**:

```lua
models.myModel:setPrimaryRenderType("END_PORTAL")
models.myModel:setSecondaryRenderType("EMISSIVE")
```

The Primary and Secondary render types get combined. You can for example set the Primary to <code>BLURRY</code> and the secondary to <code>GLINT</code> to create a model with blurry textures, while having an animated echantment glint overlayed on top of it.

---

## All Render Types

| Render Type             | Description                                                                                                      | Example Image                                                                                                                   |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `NONE`                  | Invisible                                                                                                        | <img src={require("@site/static/img/rendertypes/NONE.png").default} width="200"/>                                               |
| `CUTOUT`                | Normal, transparency in the texture is binary. Either fully invisible at an alpha of 0, or fully visible         | <img width="200" alt="CUTOUT" src={require("@site/static/img/rendertypes/CUTOUT.png").default} />                               |
| `CUTOUT_CULL`           | Normal (No Inside Faces), same alpha behavior as CUTOUT                                                          | <img width="200" alt="CUTOUT CULL" src={require("@site/static/img/rendertypes/CUTOUT_CULL.png").default} />                     |
| `TRANSLUCENT`           | Normal, with alpha values in the textures handled in a way that allows for semi-transparency                     | <img width="200" alt="TRANSLUCENT" src={require("@site/static/img/rendertypes/TRANSLUCENT.png").default} />                     |
| `TRANSLUCENT_CULL`      | Normal (No Inside Faces), same alpha behavior as TRANSLUCENT                                                     | <img width="200" alt="TRANSLUCENT_CULL" src={require("@site/static/img/rendertypes/TRANSLUCENT_CULL.png").default} />           |
| `EMISSIVE`              | Fully Lit, TRANSLUCENT alpha                                                                                     | <img width="200" alt="EMISSIVE" src={require("@site/static/img/rendertypes/EMISSIVE.png").default} />                           |
| `EMISSIVE_SOLID`        | Fullbright (No Inside Faces), CUTOUT alpha                                                                       | <img width="200" alt="EMISSIVE SOLID" src={require("@site/static/img/rendertypes/EMISSIVE_SOLID.png").default} />               |
| `CUTOUT_EMISSIVE_SOLID` | Fullbright, TRANSLUCENT alpha                                                                                    | <img width="200" alt="CUTOUT EMISSIVE SOLID" src={require("@site/static/img/rendertypes/CUTOUT_EMISSIVE_SOLID.png").default} /> |
| `EYES`                  | Fullbright, always semi-transparent, CUTOUT alpha                                                                | <img width="200" alt="EYES" src={require("@site/static/img/rendertypes/EYES.png").default} />                                   |
| `END_PORTAL`            | No-perspective End Portal Effect                                                                                 | <img width="200" alt="END PORTAL" src={require("@site/static/img/rendertypes/END_PORTAL.png").default} />                       |
| `END_GATEWAY`           | No-perspective End Gateway Effect                                                                                | <img width="200" alt="END GATEWAY" src={require("@site/static/img/rendertypes/END_GATEWAY.png").default} />                     |
| `TEXTURED_PORTAL`       | No-perspective Geometric Effect (when used as secondary rendertype, uses secondary texture to change the effect) | <img width="200" alt="TEXTURED PORTAL" src={require("@site/static/img/rendertypes/TEXTURED_PORTAL.png").default} />             |
| `GLINT`                 | Enchantment glint when used as secondary render type                                                             | <img width="200" alt="GLINT" src={require("@site/static/img/rendertypes/GLINT.png").default} />                                 |
| `GLINT2`                | Detailed enchantment glint when used as secondary render type                                                    | <img width="200" alt="GLINT 2" src={require("@site/static/img/rendertypes/GLINT2.png").default} />                              |
| `TEXTURED_GLINT`        | Uses secondary texture as enchantment glint when used as secondary render type                                   | <img width="200" alt="TEXTURED GLINT" src={require("@site/static/img/rendertypes/TEXTURED_GLINT.png").default} />               |
| `LINES`                 | White Lines Around Edges                                                                                         | <img width="200" alt="LINES" src={require("@site/static/img/rendertypes/LINES.png").default} />                                 |
| `LINES_STRIP`           | White Lines Between Vertices                                                                                     | <img width="200" alt="LINES_STRIP" src={require("@site/static/img/rendertypes/LINES_STRIP.png").default} />                     |
| `SOLID`                 | Fully white                                                                                                      | <img width="200" alt="SOLID" src={require("@site/static/img/rendertypes/SOLID.png").default} />                                 |
| `BLURRY`                | Smoothed texture                                                                                                 | <img width="200" alt="BLURRY" src={require("@site/static/img/rendertypes/BLURRY.png").default} />                               |
