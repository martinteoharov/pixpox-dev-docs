
PixPox is inspired by the roguelike [Noita](https://store.steampowered.com/app/881100/Noita/).

The aim is to provide game developers with the essentials tools for creating games similar to the aformentioned. The Cellular Automaton computation is optimized to run on the CPU making use of multi-threading for parallelization. No GPU acceleration has been or is planned to be implemented in the context of CA. 


## Overview of design; Main concepts

PixPox will be comprised of a rendering engine (based on WGPU), an Entity Component System (ECS), and a Cellular Automaton manager/helper.

There is a possibility that raytracing lighting will also be implemented.


### PixelMaps and object representation

The primary data structure for representing the game world in PixPox is the PixelMap. All components that intend to interact with the game world must implement a PixelMap.

The use of the PixelMap data structure greatly simplifies collision detection and physics calculations. For instance, to detect collisions between two PixelMaps, one could simply perform a XOR operation on the two objects to obtain the overlapping region. Based on this information, the physics system can calculate force vectors.

The developer also has to create a GlobalPixelMap which is passed to the Renderer. The GlobalPixelMap must implement a render method that accepts several arguments to allow for customization of how the GlobalPixelMap renders to the window. It is recommended that the GlobalPixelMap maintains a global representation of the game world that other components can write to.

### Entity Component System

The Entity Component System consists of three main parts: entities, components, and systems. An entity is an object in the game world that has a unique identifier. Components are individual attributes that make up an entity, such as position or health. Finally, systems operate on one or more components, allowing entities to move, interact, or behave in some specified way.

The primary benefit of using an Entity Component System in game development is that it allows for greater flexibility and reusability of code. By separating entities into their component parts, game developers can create more modular and extensible code that can be more easily modified and reused across different types of games.

Additionally, the separation of components in an Entity Component System also simplifies parallelization, which can lead to improved performance. Since each system is responsible for processing one or more components, they can be run independently in parallel. This allows for improved CPU utilization and overall system performance.

PixPox's implementation of the Entity Component System pattern is unique in that every component implements its own system. This differs from more common implementations of ECS, where systems are typically implemented independently of the components. At present, there is no way to create a system that is not attached to a component in PixPox. Despite this difference, the core benefits of the Entity Component System pattern, such as improved abstraction and parallelization, still apply to PixPox.

There are additional aspects related to the ECS implementation that merit discussion, such as queries, storage systems, mutexes, and parallelization. However, these will be detailed on a separate page.

### Rendering

The renderer in PixPox is simply a 2D texture that is passed to the GPU. Any changes to the game world are written to the texture as needed. Currently, PixPox uses an open-source project called "pixels" to simplify the rendering process. However, in future development stages, a renderer will be implemented from the ground up to better fit the specific needs of PixPox.


### Physics

PixPox features two virtual worlds when it comes to physics: one for cellular automaton (CA) interactions and one for Newtonian physics. A component can exist in either the realm of CA or Newtonian physics, although both systems are capable of interacting with each other, but on a more primitive level.

In PixPox, the behavior of certain objects, such as the player, is determined by Newtonian physics, while other objects, such as a pool of water, use cellular automata to simulate behavior. The interaction between objects in different realms is facilitated by a simple collider that prevents the two objects from occupying the same space but allows them to be positioned side by side for example.