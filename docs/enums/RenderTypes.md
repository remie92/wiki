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

| Render Type             | Description                        | Example Image
| ----------------------- | ---------------------------------- | --------------------|
| `NONE`                  | Invisible                          |   <img width="200"  alt="NONE" src="https://github.com/user-attachments/assets/9921034d-2b1c-460b-8685-4114afcfc51a" /> |
| `CUTOUT`                | Normal, transparency in the texture is binary. Either fully invisible at an alpha of 0, or fully visible| <img width="200"  alt="CUTOUT" src="https://github.com/user-attachments/assets/5736abe2-2241-4e90-bc4c-6f7fedf61bc8" /> |
| `CUTOUT_CULL`           | Normal (No Inside Faces), same alpha behavior as CUTOUT|  <img width="200"  alt="CUTOUT CULL" src="https://github.com/user-attachments/assets/b96db634-c0db-40ea-a914-c1dcbec505f3" /> |
| `TRANSLUCENT`           | Normal, with alpha values in the textures handled in a way that allows for semi-transparency |  <img width="200"  alt="TRANSLUCENT" src="https://github.com/user-attachments/assets/b528ec1c-a968-46ed-875d-6e37f65f1774" /> |
| `TRANSLUCENT_CULL`      | Normal (No Inside Faces), same alpha behavior as TRANSLUCENT| <img width="200"  alt="TRANSLUCENT_CULL" src="https://github.com/user-attachments/assets/3c6221b5-2fb2-43f5-95a3-b5c1efdc2772" /> |
| `EMISSIVE`              | Fully Lit, TRANSLUCENT alpha            |  <img width="200"  alt="EMISSIVE" src="https://github.com/user-attachments/assets/a881ac7a-4bc9-4735-969a-d76e023e840a" /> |
| `EMISSIVE_SOLID`        | Fullbright (No Inside Faces), CUTOUT alpha        |  <img width="200"  alt="EMISSIVE SOLID" src="https://github.com/user-attachments/assets/511d8bf5-3979-4068-b8b7-5e0c49aa4614" /> |
| `CUTOUT_EMISSIVE_SOLID` | Fullbright, TRANSLUCENT alpha                          |  <img width="200"  alt="CUTOUT EMISSIVE SOLID" src="https://github.com/user-attachments/assets/27b4ee02-d2ca-46f3-8904-3ec9f50b5860" /> |
| `EYES`                  | Fullbright, always semi-transparent, CUTOUT alpha            |  <img width="200"  alt="EYES" src="https://github.com/user-attachments/assets/d95c3b21-2bd9-4385-801c-36899e9bcac3" />  |
| `END_PORTAL`            | No-perspective End Portal Effect  |  <img width="200"  alt="END PORTAL" src="https://github.com/user-attachments/assets/3293c8ea-920b-4330-8a15-e02219c47df9" /> |
| `END_GATEWAY`           | No-perspective End Gateway Effect |  <img width="200"  alt="END GATEWAY" src="https://github.com/user-attachments/assets/531b3d7d-370d-4754-82de-8c28c1be7243" /> |
| `TEXTURED_PORTAL`       | No-perspective Geometric Effect (when used as secondary rendertype, uses secondary texture to change the effect)  |  <img width="200"  alt="TEXTURED PORTAL" src="https://github.com/user-attachments/assets/a4d551e6-7284-4131-bcc5-646d55534448" /> |
| `GLINT`                 | Enchantment glint when used as secondary render type|  <img width="200"  alt="GLINT" src="https://github.com/user-attachments/assets/adb7db34-fe42-43c8-aa73-bb6af0ac8669" /> |
| `GLINT2`                | Detailed enchantment glint when used as secondary render type|  <img width="200"  alt="GLINT 2" src="https://github.com/user-attachments/assets/e1b93d1a-e126-4316-b282-ef7b6716cada" /> |
| `TEXTURED_GLINT`        | Uses secondary texture as enchantment glint when used as secondary render type|  <img width="200"  alt="TEXTURED GLINT" src="https://github.com/user-attachments/assets/bdcecf93-bfbc-4d61-ac2e-367fa2b444cd" /> |
| `LINES`                 | White Lines Around Edges         |  <img width="200"  alt="LINES" src="https://github.com/user-attachments/assets/136b0492-6bf0-4b48-8519-4cc1c31f5ed8" /> |
| `LINES_STRIP`           | White Lines Between Vertices     |  <img width="200"  alt="LINES_STRIP" src="https://github.com/user-attachments/assets/5a9307c6-71ae-4c37-b59b-1b2afbe48f18" /> |
| `SOLID`                 | Fully white |  <img width="200"  alt="SOLID" src="https://github.com/user-attachments/assets/1c3500db-1c21-45f7-b856-7f11af5c57f6" /> |
| `BLURRY`                | Smoothed texture                   |  <img width="200"  alt="BLURRY" src="https://github.com/user-attachments/assets/72fabc5e-244b-4c87-9dfe-0604abfae378" /> |


