---
layout: section
transition: null
---

# My first attempt

Wrapping Wasmer's C-API

---

## Wrapping Wasmer's C-API

with a React Native Nitro native module

- React Native native module (using Nitro) calling from C++ into the Wasmer C-API (wasm.h)
- A JavaScript wrapper calling into the native module

Caveats

- I'm not an expert of Wasmer nor Nitro modules

<!--

- My failed naive attempt: Exposing Wasmer as a Nitro Module. [Kræn]
  - Show some architecture and code.
  - Highlight the challenges (missing features, docs, etc.)
  - 400ms (adding two numbers 1mio times)
  - Found Polygen and became an early adopter of Polygen
-->

---
src: ./benchmark-results.md
---

# Takeaways

- While very fast,
