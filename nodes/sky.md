---
category: [nodes]
description: Provides an environment texture for the stage.
---

# Sky

Sets the environment texture for the stage the node belongs to.

In raster rendering, the provided environment texture is used for specular environment reflections as well as ambient irradiance.

In raytraced rendering, the environment texture is used for sampling radiance from the sky when a ray misses all geometry.


!!!warning
Right now, the sky node only works with equirectangular environment textures.
!!!
