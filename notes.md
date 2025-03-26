## Pitch

As building cross-platform mobile and desktop apps in React Native is ever increasing. As the ecosystem is closing the gap towards Web-APIs, it is increasingly feasible to build performant and truly universal apps and libraries.

The latest advancement: Executing WASM in React Native apps ⚡️📲

---

As building cross-platform mobile and desktop apps in React Native (OSS by Meta) is ever increasing. As the ecosystem is closing the gap towards Web-APIs, it is increasingly feasible to build performant and truly universal apps and libraries. The latest advancement is the ability to execute WASM in a React Native app.

In this talk, I’ll start from my naive approach of implementing a native module for React Native, exposing the Wasmer runtime, which turned out to be really slow, mainly because of the restriction on iOS devices that apps are not allowed to perform just-in-time compilation on devices. This however is balanced with the React Native platform’s ability to run ahead-of-time compiled native code and the current solution, built and maintained by Callstack, uses wasm2c to build native modules for React Native.

---

I am an active maintainer of Realm JS (a local-first database for Node.js and React Native) and frequent contributor to both React Native and other libraries in the ecosystem. I’ve also been prototyping a wrapper of the Wasmer runtime for React Native, compiling Rust to binaries for iOS and Android and interfacing with this via a C-API, but choose to pause work on it as I realized the performance penalty endured on iOS and as I learned about the advancements that was made elsewhere in the ecosystem.

## TODO

- Kræn runs a fibonacci "benchmark":
  - One invocation doing a lot of work.
  - Many invocations doing a little work.
On:
  - Safari
  - Wasmer (no JIT)
  - Polygen AOT

## Limits

Your session: standard talks are 30min long, we recommend leaving some minutes for Q&A but that's up to you.

## Outline

- WebAssembly is not everywhere.
- About us (2 min)
 - Kræn [Kræn]
 - Robert [Robert]
- Motivation
  - Why React Native and what makes it special (in this context)? [Kræn] (5 min)
    - Widely adopted (perhaps highlight Expo numbers?)
      - Using a known and popular stack React + JavaScript
      - Backed by Meta
      - Large ecosystem
        - https://reactnative.directory/
        - Numbers?
    - Native first (not a web-view):
      - Exposing native UI components rather than re-inventing them (as opposed to Flutter, Cordova)
      - Limited web-APIs available.
    - No JIT to machine-code in iOS apps
    - Luxury of ahead-of-time build step (as opposed to the Web)

---

  - Why WASM in React Native? [Robert] (5 min)
    - Why not? We don't need it.
    - A future of universal apps and libraries:
      - Having a single target for native modules (across OS, architectures and web) is awesome.
      - Libraries with existing WASM targets.
    - A good alternative to TurboModules: (existing library already targeting React Native)
      - Targeting a single architecture.
      - A generic ABI, not specific to the library.

---

(3 min)

- My failed naive attempt: Exposing Wasmer as a Nitro Module. [Kræn]
  - Show some architecture and code.
  - Highlight the challenges (missing features, docs, etc.)
  - 400ms (adding two numbers 1mio times)
  - Found Polygen and became an early adopter of Polygen

---

(10 min)

- Polygen [Robert]
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

(5 minutes)

- CTA
 - You can ship WASM for React Native (Still early)
 - What future would you like to see?
 - Let's collaborate on bringing your libraries onto React Native.
 - Questions?
