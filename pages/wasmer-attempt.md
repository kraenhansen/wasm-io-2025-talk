---
layout: section
transition: null
---

# My first attempt

Wrapping the Wasmer C-API

<!--
Kræn for 3 minutes.
I'll now share some experiences from my first attempt or proof-of-concept to bring WebAssembly to React Native.
Wrapping the Wasmer C-API in a React Native Nitro module.
-->

---

## Wrapping the Wasmer C-API

with a React Native Nitro native module

<v-clicks>

- A TypeScript wrapper calling into a native module
- A native (Nitro) module calling from C++ into the Wasmer C-API (wasm.h)
- A small build CLI wrapping the Cargo CLI and Xcode build tools, to produce an XCFramework.
- 👀 Very limited subset of the WebAssembly API surface (for now)
- 👀 iOS only (for now)
- 👀 I'm not an expert of Wasmer nor Nitro modules

<!--
I built a simple TypeScript wrapper calling into a Nitro module.
[click] the Nitro module, call from C++ into the Wasmer C-API (wasm.h)
[click] a CLI builds Wasmer for iOS into an XCFramework.
[click] Note: Very limited subset of the WebAssembly API surface.
[click] Note: Worked on iOS only.
[click] Note: Don't take the benchmark results too literally - I didn't spent weeks optimizing it and I don't claim to be an export on neither Wasmer nor Nitro modules.
-->

</v-clicks>

---
layout: full
transition: null
---

<BenchmarkResults xMaximum="5" filterSeries="['Wasmer using JSC']" />

<!--
Never the less, these were my initial results:
About 360.000 ops/s computing low fibonacci numbers.
I was pretty happy about that.
-->

---
layout: full
transition: null
---

<BenchmarkResults xMaximum="5" filterSeries="['Wasmer using JSC', 'Safari']" />

<!--
Until I compared to Safari and saw this.
This was where I resurfaced and looked around for alternatives and learned that Callstack was also building something, leveraging AOT compilation.
-->

---
layout: full
transition: null
---

<BenchmarkResults filterSeries="['Wasmer using JSC', 'Safari']" />

<!--
If I would have spent a bit more time on benchmarks however,
I would have learned that most of my performance issues were from the code calling into Wasmer.
-->

# Takeaways

<v-clicks>

- Wasmer is fast
- JIT can be avoided, using Wasmer's JavaScriptCore feature
- Not fun to build one side of a C-bridge (as a TypeScript developer)

</v-clicks>

<!--
Wasmer is fast
[click] JIT can be avoided, using Wasmer's JavaScriptCore feature
[click] It's not fun for a TypeScript developer to maintain one side of a C-bridge.
-->
