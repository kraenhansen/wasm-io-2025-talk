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

And we want to introduce our newest project, Polygen.
It fresh off the oven, [click] still experimental.
-->

---

# Polygen

What is it?

<v-clicks depth="2">

- Provides WebAssembly support for React Native
  - Highly performant
  - WebAPI compatible
- Alternative to TurboModules
  - Simplifies embedding of third party modules 

</v-clicks>

<!--
[click] Polygen is our new approach to running WebAssembly in React Native. 

[click] It is a highly performant solution that uses codegen (more on that in a second),

[click] that is compatible with the WebAPI, we all know and love.

[click] It can be seen as an alternative to TurboModules.

[click] It simplifies consuming and embedding of third party modules, a lot .
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

So let's talk a bit about how it works.

[click] As I mentioned before it is really fast, achieving near native performance.

[click] This is because it compiles WebAssembly to C, using the all wonderful `wasm2c` tool, from WebAssembly Binary Toolkit.

[click] To connect it with React Native, the generated code is glued with JSI (JavaScript interface). This glue code is also generated

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
  - Rust | Go in the core, React/TypeScript in the UI

</v-clicks>

<!--

[click] It is truly universal. Your apps work on Web and native seamlessly.

[click] You can use existing WebAssembly ecosystem in React Native. One of such examples is a crypto library, 
which is not provided in react native out of the box.

[click] Finally, you can extend react native functionality with languages other than C++,
or write business logic.

By the way, the project name comes from the word "polyglot" and "codegen".

[click] Any language that compiles into WASM can be used, obviously.
We get best of both worlds, React for UI, the language you like for business logic.
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

<!--
[click] So lets say you have a web app
[click] You native webassembly modules, for advanced computations
[click] You want to make a mobile app of it
[click] Polygen allows you to do that
-->

---

# Polygen

Bringing your React Native App to Web

<v-clicks depth="2">

- You have a React Native App
  - You need native functionality (e.g. TurboModules)
- You want to make a Web app version
- Polygen allows you to do that

</v-clicks>

<!--
[click] So lets say you have a RN app
[click] You need to use native functionality, using TurboModules
[click] You want to make a web app version of it
[click] TurboModules are RN only, webassembly saves the day!
-->

---

<BenchmarkResults filterSeries="['Wasmer using JSC', 'Safari', 'Polygen']" />

<!--

As you can see, polygen does pretty well thanks to wasm2c performance.
There's some calling overhead at the lower fibonacci sequences, but it outperforms safari slightly at higher numbers.

There's still a room for improvements, but it's a good start.
We can probably squeeze some more performance out of it.

-->

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
[click] like wasmer [click] wasmtime and [click] more.

Mostly for Android or desktop platforms, due to JIT limitations on IOS.
-->

---

# Future plans

<v-click>

<p>WebAssembly Mobile Interface (WAMI)</p>

</v-click>

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

<v-click>
 
```wit
interface notification {
    record Notification {
        // ...
    }
    
    show-notification: func(event: Notification) -> result<NotificationHandle>;
}
```

</v-click>

<!--
There are many more opportunities for the future we want to play with and discover.

[click] One of those areas are WebAssembly components. We could use WIT to
expose UI APIs to webassembly modules to allow us to write the apps in various languages.

[click] Imagine system's calendar API exposed to webassembly module using WIT.
Calendars are available in mobile devices and desktop platforms.  

[click] Or, as an alternative example, consider Notifications API.
-->

---

# The future

<div style="display: flex; flex-direction: row; justify-content: space-between; gap: 10px;">

<div>

### C
```c
#include "wami/notifications.h"

void on_click() {
    wami_notification_t notification;
    notification.title = "Test";
    
    wami_notification_show_notification(&notification);
}
```

</div>
<div>

### Rust
```rust
use bindings::webapi::wami::notifications::Notification;
use bindings::webapi::wami::notifications::show_notification;

fn on_click() {
    let result = show_notification(Notification { 
        title: "Test!"
        // ... 
    });
}
```

</div>

</div>

<!--

Imagine using system's native APIs, from Rust or C accessed
through WebAssembly interface.

-->

---

# WebAPIs

<v-click>
The IDLs are already there!
</v-click>

<v-click>
 
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

</v-click>

<!--

Let's quickly talk about WebAPIs.

[click] The WebAPIs are already defined using IDL called WebIDL.

[click] Here's an example of a snippet of web crypto API.

So imagine writing native apps, in rust, using WebAPIs
without the browser.

We could, for example, generate WITs from WebIDL.
-->