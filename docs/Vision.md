
PixPox is inspired by the roguelike [Noita](https://store.steampowered.com/app/881100/Noita/).

The aim is to provide game developers with the basics for creating games similar to the above mentioned Noita. It should also be capable of running on potato hardware.


- Data Structures
	- Pixelmaps
		- Collision
		- Physics System (acceleration, velocity, mass, momentum, etc.)
- Interaction
	- Cellular Automaton based interaction
		- Simple definition of rules
		- Optimizations
- 

### The Parts

PixPox will be comprised of a rendering engine (based on WGPU), a physics engine (written from scratch) and a cellular automaton manager. 

If I have enough time it will also feature a 2D raytracing lighting.

## Data Structures

### PixelMap

The main datastructure used for representation in the world will be a PixelMap.
It simply holds the raw pixel data representation of the object in a map. 

This data format will make collision detection and physics calculation very fast and easy. For example - in order to detect a collision between two PixelMaps, you will very simply just XOR the two objects to get the overlapping area. Based on the overlapping area you could calculate force vectors for the physics system.


## Entity Component System

## Rendering

## Physics

