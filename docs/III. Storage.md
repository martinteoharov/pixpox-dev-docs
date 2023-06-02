The Storage system is designed to manage and maintain global data in the context of the entity component system. It employs a HashMap data structure to store developer-defined data of any type in buckets, and offers a comprehensive query system to facilitate the creation and retrieval of said buckets.

The storage also uses a multi-threaded interner to efficiently store bucket labels and associate them with Spur keys, which can be used to efficiently look up data in the HashMap.

## How it is built

### Query System



### Mutability

### Philosophies

