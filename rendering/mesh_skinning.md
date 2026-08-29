# Mesh Skinning

Because Cinebara combines raster rendering with raytracing, a deformed mesh needs geometry that both systems can read. The intended design gives every deformable mesh instance its own deformed position, normal, and optional tangent buffers. A mesh can then pass through ordered, cacheable deformation stages such as bone skinning, blendshapes, and procedural effects.

# Blendshapes

!!!warning
Blendshapes and morph targets are part of the intended deformation pipeline. They are not implemented in the current state of the engine.
!!!

Also referred to as "Shape Keys" or "Morph Targets", blendshapes are a big list of per-vertex offsets that can be linearly applied to a mesh to control the surface, allowing the mouth to move for making visemes,  customize the source mesh in an artistic way, or correct for distortions introduced during bone transformation.

Blendshapes are stored alongside the mesh in 3 buffers: One for vertex indices, one for position and normal offsets, and finally one which describes the slices of the index buffer to use for each blendshape. The weights for an instance of the mesh would be supplied in the object group, like the model matrix.

# Bone transforms

Each vertex index in a mesh is associated to a list of bone indices and weights. Since we're aiming for film quality, the typical 4 bone per-vertex limit is not fit. Instead, a flexible structure is used where each vertex is given a slice into 2 buffers, one for bone indices and one for bone weights. This feels similar to how Bindless describes meshes with slices into a large global buffer. Not only does this approach allow for an unbounded number of weights per-vertex, but also compresses data when vertices have few weights.

The list of bone transforms that compose a Skeleton are then also supplied, a packed list of 4x4 matrices describing object-space transforms. This means that moving a Node that is a parent of a skinned mesh does not require re-computing all of the bone matrices.

Only positions, normals, and tangents are transformed by this process, meaning two skinned mesh instances that use the same mesh will share their colors, texture coordinates, and anything else that is not dependant on transformation. Unfortunately, this does mean that memory usage is not as optimal as in traditional vertex program based processes, but since it allows for raytracing, the tradeoff is required.

# Procedural Effects

Some graphical effects require applying arbitrary transformations to the vertices of a Mesh. This is also done in the skinning phase before any real rendering. This is where soft surfaces are processed. The specific method for this stage depends on the required effect, so use the prior sections as fuel for your imagination as to what could be done here.
