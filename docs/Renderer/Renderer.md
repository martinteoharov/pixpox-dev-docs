
The PixPox renderer will be written from scratch and will, in practice, act as a wrapper for WGPU (which is a low-level rendering library that is one abstraction above OpenGL, Vulkan and other backends).

This file contains all of the approaches I have taken to:
- translate world data to renderer language
- represent both world and renderer data efficiently
- achieve optimal running time
- have raytracing for lighting

I will be documenting the process as I go along.


## The vision

In PixPox most of the entities and game components are represented using pixels. Large objects such as terrain are simply PixelMaps with a texture attached to them. Active cellular entities are simply just a pixel - a 2D coordinate with a color attached to it. 

All of these objects are represented as entities in the world structure.

The perfect renderer for pixpox will have the following features:
- Pixel manager
- Batch rendering









## Tasks:

- [ ] 2D Renderer
	- [ ] Scene
	- [ ] BitMaps
	- [ ] Geometry?
	- [ ] Textures?
	- [ ] Utilities
		- [ ] Math
	- [ ] Renderer


