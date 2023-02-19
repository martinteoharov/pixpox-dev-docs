
Entity Component System (ECS) is a design pattern responsible for representing the world and its various objects (player, light, physics, etc..). An ECS comprises of entities, which are composed of components and lastly systems which operate on said entities.

This design pattern allows us to build logic that is incredibly flexible while also being immensely performative. it is the best choice for a complicated game engine full of various interconnected behaviour.

## How it is built

### Entities

-  Unique Identifiers

	Every entity has a unique identifier associated with it. 
	IDs start from 0 and increment by 1 on every new entity created. The ID value currently does not decrement on entity removal, since it is unnessecary. A better future implementation will include a Queue datastructure to get the smallest possible ID for a new entity. Currently if you remove entity with id 10, the next creation of entity wouldn't fill the missing gap but just move on to id 11 or whatever the biggest id+ 1 is.



### Components

- World representation

	Components are stored in the world in a `Vec<Box<dyn ComponentVec>>` structure. The data-type is basically a Vector of Heap allocated Vector.



-  Systems




### Rust TypeSystem integration


