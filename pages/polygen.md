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

<v-clicks depth="2">

- Provides WebAssembly support for React Native
  - Highly performant
  - WebAPI compatible
- Alternative to TurboModules

</v-clicks>

<!--
[click] Polygen is our new approach to running WebAssembly in React Native. 
[click] It is a highly performant solution (more on that in a second), that is compatible with the WebAPI. 
[click] It is an alternative to TurboModules.
-->

---

# Polygen

How it works?

<v-clicks depth="2">

- Compiles WebAssembly to C code
  - Using the wonderful WABT `wasm2c` tool 
- Generates additional JavaScript Interface (JSI) glue-code
- AOT compilation allows for near-native performance
- WebAssembly code is linked with the application
  - No JIT means it can be used in iOS apps

</v-clicks>

<!--
[click] It is super-fast, [click] because it compiles WebAssembly to C using the all wonderful `wasm2c` tool, from WebAssembly Binary Toolkit.

[click] To connect it with React Native, the generated code is glued with JSI (JavaScript interface)

[click] Ahead of time compilation allows for near native performance.

[click] The resulting code becomes part of the application, just like a normal native static or shared library.

[click] Also, we decided to use this approach so that it can be deployed in iOS apps, where JIT is not allowed.
-->

---

# Polygen

What it enables?

<v-clicks depth="2">

- Write universal (native & web) apps with ease
  - Bringing React Web apps to Native
  - Bringing Native apps to Web
- Brings WebAssembly library ecosystem to React Native
- Writing Polyglot business logic
  - Rust|Go in the core, React/TypeScript in the UI

</v-clicks>

<!--
[click] It is truly universal.

[click] You can easily bring your web app to native, [click] or your native app to the web.

[click] You can use existing WebAssembly libraries in React Native. One of such examples is a crypto library, which is not provided in react native.

[click] Finally, you can extend react native functionality with languages other than C++

[click] Any language that compiles into WASM can be used, obviously.
-->

---

# Future plans

<v-clicks depth="2">

 - Complete support for WASM features
   - Threading, SIMD, ...
 - WebAssembly Mobile Interface (WAMI?)
   - Notifications
   - Contacts
   - Location
   - ...
 - Multiple runtimes (wasmer, wasmtime)

</v-clicks>

<!--
[click] Bring support for missing or untested WASM features.
[click]

[click] Expose mobile app interface to WebAssembly modules.
[click] [click] [click] [click]

[click] Add support for more WASM runtimes (mostly for Android or desktop platforms)

-->