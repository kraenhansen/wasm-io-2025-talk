---
layout: section
transition: null
---

# Polygen

<!--
- Wrapping the WebAssembly Binary Toolkit's `wasm2c` (matches the AOT capabilities of React Native)
- Code generation of a JSI bridge to expose imports and exports
- Compatible with the web API
- Near native performance (because it's C)
  - (Benchmark result?)
- Limitations?
  - Threading
- Examples:
  - Crypto
  - ...
- Future improvements: [Robert]
  - WASI for mobile (WAMI)?
  - Support for WebAssembly Components?
  - What do you think?
-->

---

# Polygen

What is it?

<v-clicks>

- WebAssembly support for React Native
  - Highly performant
  - WebAPI compatible
- Alternative to TurboModules

</v-clicks>

---

# Polygen

How it works?

<v-clicks>

- Compiles WebAssembly to C code
  - Using the wonderful WABT `wasm2c` tool 
- Generates additional React Native glue code
- AOT approach allows for near-native performance
- WebAssembly code is linked with the application
  - No JIT means it can be used in iOS apps

</v-clicks>


---

# Polygen

What it enables?

<v-clicks>

- Write universal (native & web) apps with ease
- Simplifies integration of existing native/WebAssembly libraries
- Writing Polyglot business logic
  - Rust|Go in the core, React/TypeScript in the UI

</v-clicks>

---

# Future plans

<v-clicks>

 - Complete support for WASM features
   - Threading, SIMD, ...
 - WebAssembly Mobile Interface (WAMI?)
   - Notifications
   - Contacts
   - Location
   - ...
 - Multiple runtimes (wasmer, wasmtime)

</v-clicks>