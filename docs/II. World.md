
For a summary of the concept, read [[I. Vision#Entity Component System]].

The Entity Component System (ECS) is a powerful design pattern that facilitates the representation of a game world and its myriad of objects and algorithms, such as players, lights, terrain, physics, and more. An ECS comprises of entities, which are composed of components and lastly systems which operate on said entities.

By separating entities into their individual components, developers can create a flexible and high-performing logic that's perfect for complex game engines. This approach enables the creation of modular and extensible code that's easily modified and reused across various types of games.

The separation of components in an ECS also simplifies parallelization, which can result in improved performance. Because each system is responsible for processing one or more components, they can be run independently in parallel. This leads to increased CPU utilization and enhanced overall system performance.

## How it is built

### Entities

Entities are very simple. They are basically just a number - their ID. The EntityManager struct also includes methods for creating and deleting entities.

**Fields:**

-  id

	Each entity in the game world possesses a unique identifier. These IDs start from 0 and increment by 1 for every new entity that's created. At present, the ID value doesn't decrement on entity removal, as it's deemed unnecessary. In the future, a better implementation will utilize a queue data structure to retrieve the smallest possible ID for a new entity.


### Components

Components are stored in the world in a `Vec<Box<dyn ComponentVec>>` structure, which allows for efficient memory packing. This data structure is essentially a vector of heap-allocated vectors with additional custom logic attached to the inner vector.

// TODO: Clarify this & Make sure it makes complete sense
One advantage of this approach is that it enables us to optimize memory usage by packing data tightly into the smallest amount of memory required. This is achieved by organizing the components in memory so that there are no gaps between them, which reduces the amount of unused space in memory. In addition, the use of heap-allocated vectors allows for easy dynamic allocation and modification of components as needed during runtime.

As a developer using PixPox, you have the freedom to create custom components. However, it is essential that these components implement specific traits so that they are accepted by the engine.

``` rust
pub trait Label {
    fn label(&mut self) -> &'static str;
}

pub trait Run {
    fn run(&mut self, storage: &Storage);
}

pub trait Update {
    fn update(&mut self, storage: &RwLock<Storage>);
}
```

The `Label` trait requires that every component has a `label()` method that prints out its type. This is useful for debugging purposes.

The `Run` trait specifies a `run()` method that is executed for each component whenever `world.run()` is called. This function is parallelized using multi-threading and only has read access to the storage. It is designed for heavy computation, and no updates are allowed.

The `Update` trait specifies an `update()` method, which much like `run()`  is executed on every pass of `world.run()`. It is also parallelized, but its given a `RwLock` instead of an immutable reference. This method is meant to update the world when a change is present, and it should not attempt to obtain a `.write()` lock on the storage when no changes are present, as doing so would adversely impact performance.

### Systems

In PixPox, systems are incorporated as part of the component. Every component features two mandatory system functions: `Run()` and `Update()` as discussed in the above section. During the `world.run()` call, both functions are executed.

Firstly, `Run()` is called on all components, with an immutable reference to the storage. It's important to note that the `Run()` method is not allowed to modify anything in the global storage. This approach is necessary because the `Run()` calls are parallelized.

Once all `Run()` methods have been executed, `Update()` is called on each component, with a reference to a `RWLock` that's distilled into a reference of write-access to the storage. The philosophy of the `Update()` function is all about updating the global storage. As such, it shouldn't contain any computationally intensive code.

Overall, this design ensures that all the components are processed and updated efficiently in parallel, while also safeguarding the integrity of the global storage.



### Rust Type System integration

There are many reasons why Rust is a fantastic language, one of which is its robust type system that introduces "Traits".

In Rust, a trait is a feature that defines a set of methods that a type can implement. It is similar to interfaces in other programming languages, but with additional capabilities and flexibility.

Traits provide a way to define shared behavior across different types. By implementing a trait, a type can guarantee that it has certain properties or capabilities, which allows it to be used in a more generic way. For example, the `ToString` trait can be implemented by any type that can be converted to a string, such as integers or custom structures.

Additionally, traits can be used to define default behavior for types, enabling more efficient and concise code. They can also be used to enable dynamic dispatch, which is useful for building more modular and extensible code. 

In our implementation, Traits play an essential role in determining what can be a Component. For a Component to be valid, it must implement the Traits Run, Update, and Label. Additionally, a Component can optionally implement Texture, but we will discuss that later.

In the ECS, a "Component" can be assigned to an entity by first creating a Component Type. Once the Component Type is defined, a variable of that type can be initialized and passed to the helper method `World::add_component_to_entity()`, which attaches the component to the entity.

To ensure that each entity has its own copy of the Component, we require the trait Copy, as we cannot have a reference to a single component in memory for every entity. By making Components Copy-able, we can create unique instances for each entity that has the Component attached to it.