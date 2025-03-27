---
layout: section
transition: null
---

# Polygen

<v-click>

## Still Experimental ⚠️

</v-click>

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

<!--
Robert for 10 minutes.

Fresh off the oven, [click] still experimental.
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
- Brings growing WebAssembly ecosystem to React Native
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

# Polygen

Bringing your Web App to React Native

<v-clicks depth="2">

- You have a WebApp 
  - It uses WebAssembly modules
- You want to bring it to React Native
- Polygen allows you to do that 🚀

</v-clicks>

---

# Polygen

Bringing your React Native App to Web

<v-clicks depth="2">

- You have a React Native App
  - You need native functionality (e.g. TurboModules)
- You want to make a Web app version
- Polygen allows you to do that

</v-clicks>

---

<BenchmarkResults />

---

# Future plans

<v-clicks depth="2">

 - Complete support for WASM features
   - Threading, SIMD, ...
 - Multiple runtimes
   - wasmer
   - wasmtime
   - and more

</v-clicks>

<!--
[click] Bring support for missing or untested WASM features.
[click] Threading, simd and more of them

[click] We'd love to explore adding support for more WASM runtimes,
mostly for Android or desktop platforms, due to JIT limitations on IOS.
-->

---

# Future plans

<v-click>
```wit
package wami:common;

interface calendar {
    record CalendarEvent {
        // ...
    }
    
    add-event: func(event: CalendarEvent) -> result<bool>;
}
```

</v-click>

<!--
And, thanks to the webassembly tools, we could leverage those APIs in different languages.
-->
---

# WAMI

```wit
package wami:common;

interface notification {
    record Notification {
        // ...
    }
    
    show-notification: func(event: Notification) -> result<NotificationHandle>;
}
```

<!--
Or, as an alternative example, consider Notifications API.
-->

---

# WebAPIs

```csharp
partial interface mixin WindowOrWorkerGlobalScope {
  [SameObject] readonly attribute Crypto crypto;
};

[Exposed=(Window,Worker)]
interface Crypto {
  [SecureContext] readonly attribute SubtleCrypto subtle;
  ArrayBufferView getRandomValues(ArrayBufferView array);
  [SecureContext] DOMString randomUUID();
};
```

<!--
The WebAPIs are already defined using IDL called WebIDL.
[click] Here's an example of a snippet of web crypto API.

So imagine writing native apps, in rust, using WebAPIs
without the browser. Wild.
-->

---

# 