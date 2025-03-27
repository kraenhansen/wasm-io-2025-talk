---
layout: section
transition: null
---

# My first attempt

<!--
Kræn for 3 minutes.
Now I will share the results of my first attempt at bringing WebAssembly to React Native.
-->

---

## PoC wrapping the Wasmer C-API

in a native module for React Native

<v-clicks>

- A TypeScript wrapper calling into a native module
- A native module calling from C++ into the Wasmer C-API (wasm.h)
- A small build CLI wrapping the Cargo CLI and Xcode build tools, to produce an XCFramework.
- Used the JavaScriptCore feature of Wasmer
- 👀 Very limited subset of the WebAssembly API surface (for now)
- 👀 iOS only (for now)
- 👀 I'm not an expert on Wasmer
- 💙 I'd be happy to share it

</v-clicks>

<!--
Around October of last year, I built a proof-of-concept of wrapping Wasmer in a native module for React Native.
[click] I built a simple TypeScript wrapper calling into a native module.
[click] the native module, call from C++ into the Wasmer C-API (wasm.h) - manually consuming a C-API is painful, especially as a TypeScript developer.
[click] a CLI builds Wasmer for iOS into an XCFramework.
[click] Used the JavaScriptCore feature of Wasmer, to avoid relying on JIT (talking with Syrus during the conference, this might not work in production apps and is superseded by the v8 backend)
[click] Note: Very limited subset of the WebAssembly API surface.
[click] Note: Worked on iOS only.
[click] Note: I don't claim to be an export on neither Wasmer, so you shouldn't take my benchmarks too literally - I might very well have missed opportunities for optimizations.
[click] If anyone is interested, I'd be happy to share the code - but since its in such a rough stage, it won't be public.
-->

---
layout: full
transition: null
---

<BenchmarkResults xMaximum="5" filterSeries="['Wasmer using JSC (initially)', 'Wasmer using JSC']" />

<!--
With all those caveats and reservations out of the way, these were my initial results:

Initially I saw about 360.000 ops/s, computing low fibonacci numbers and at first I was pretty happy about that.

I later managed to get 1.8 million ops/s (what you see on the graph), after tuning optimizations computing low fibonacci numbers.
I was pretty happy about that.
-->

---
layout: full
transition: null
---

<BenchmarkResults xMaximum="5" filterSeries="['Wasmer using JSC', 'Safari']" />

<!--
Until I compared to Safari and saw that it did 23 million ops/s.

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

---

# Takeaways

<v-clicks>

- Wasmer is fast
- The JS wrapper + JS into Wasmer dominates the benchmark results for small workloads
- AOT and JIT can be tuned, using specific Wasmer's backends
- Not fun to build one side of a C-bridge (as a TypeScript developer)
- Callstack was making a lot of great progress on Polygen

</v-clicks>

<!--
[click] Wasmer is fast
[click] JIT can be avoided, using specific Wasmer's backends
[click] It's not fun for a TypeScript developer to maintain one side of a C-bridge.
-->
