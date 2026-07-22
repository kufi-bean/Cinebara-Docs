# Render Functions
A Render Function handles the rendering for one kind of shader. Mesh Renderers automaticallly register themselves to the [Render Scene](#render-scene) using the Render Function of the supplied shader. A Render Function's responsibilities depend on what kind of shader is being rendered. For example, a Bindless Render Function is responsible for collectin all of the information used in Bindless Rendering. Many Shaders may share one Render Function, and then it is up to the Render Function to decide what to do with each shader used.

This architecture allows for many meshes to be drawn at the same time, entirely dependent on the implementation of the Render Function. It also allows for drawing things one at a time, unconstrained by any optimization surface. It allows for hybrid rendering styles between Deferred and Forward.

!!!question Is it deferred?
Does it really support deferred rendering? It is highly based on the Render Function to decide what data to produce or process, how can they work with eachother and share buffers?
!!!

# Render Data (Elements)
Each Render Function is associate to a list of elements to Render. Each of these elements is often referred to as `RenderData`. As an example, `BindlessRenderData` holds a mesh, bindless material, transform, and a bounding box. Different Render Functions will want different data, so this structure supports that arbitrary nature. This concept exists because of the Render Thread being decoupled from the Engine Thread; a Render Function can't just read the Mesh Renderer to get its location or mesh as that may lead to race conditions. Instead, updating the Render Data is done in a deferred call, often operating on locally captured variables for thread safety. These deferred calls are typically done during `Node.onPrepareRender`.

The Render Data required is entirely dependant on the Render Function being used, whioch is supplied by the Shader being used. It is therefor the responsibility of the Shader to define how to turn a MeshRenderer into Render Data.