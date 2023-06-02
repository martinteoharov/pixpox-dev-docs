
### Game Engine

- [ ] Architecture
	- [x] Create pixpox_common
	- [x] Integrate the GlobalPixelMap into the engine
	- [ ] Provide an API for the GlobalPixelMap
	- [ ] Compile to WASM
	- [ ] Cell Realm
		- [ ] Make a way for Cells to define their behaviour
		- [ ] Think of an API that lets the developer define behaviour easily
		- [ ] Document
- [ ] Chores
	- [ ] Clean code up
		- [ ] Find a way to remove all unnecessary imports
		- [ ] Define rules for linting and formatting (alphabetical imports, remove unnecessary imports)
	- [ ] Fix ECS and Conway examples
	- [ ] Benchmarks for Cell Realm
	- [ ] Suite of tests for the whole repo
	- [ ] Update docs with some shit from the dissertation document
- [ ] Features
	- [ ] State serialisation 
	- [ ] Level builder
	- [ ] Newtonian physics
	- [ ] Texture system
		- [ ] Components must implement texture trait
		- [ ] Components can have textures attached to them that can be rendered
- [ ] Fixes
	- [ ] GUI out of bounds