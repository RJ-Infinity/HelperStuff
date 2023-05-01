# Realy Simple Memory Allocator for wasm

all the other options were in massive libraries or hundreds of lines long this is under 100

## how to use
first add atribution to your project

then copy it in and load in any way you wish

```js
// then create an instance
const memAllocer = new memAlloc();

// read in and load the WASM file
const WASMFILE = await WebAssembly.instantiateStreaming(fetch("/build/automota.wasm"), {env:{
	// you must add the methods from the class bound or they will fail
	"malloc":memAllocer.alloc.bind(memAllocer),
	"free":memAllocer.free.bind(memAllocer),
}});

// then add a reference to the WASM's memory
memAllocer.setMemory(WASMFILE.instance.exports.memory);
//this must be done before you run any functions that malloc

// i got the memory from exporting
// you can also get your memory by createing it and passing it to the wasm
// https://developer.mozilla.org/en-US/docs/WebAssembly/JavaScript_interface/Memory

```

this is almost definitly not the best fastest or most efficient memory allocator for WASM
as i have done almost no reasearch on how one would create that product but it does work
and it shouldnt create massive memory leaks 🤞 it was made to be small and thats about it
