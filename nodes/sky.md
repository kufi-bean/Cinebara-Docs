---
category: [nodes]
description: Provides an environment texture for the stage.
---

# Sky

When in a stage, sets the environment texture for the stage. An environment texture is used in raster rendering for default ambient irradiance as well as in raytracing when a ray hits no geometry. An irradiance cubemap is computed any time the environment texture is updated. Updating the environment texture is expensive as a full irradiance convolution has to run to calculate the irradiance cubemap.

Right now, the sky node only works with equirectangular environment textures.