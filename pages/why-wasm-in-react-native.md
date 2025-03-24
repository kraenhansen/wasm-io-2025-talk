---
layout: section
transition: null
---

# Why WASM in React Native?

<!--
(5 min)
- A future of universal apps and libraries:
  - Having a single target for native modules (across OS, architectures and web) is awesome.
  - Libraries with existing WASM targets.
- A good alternative to TurboModules: (existing library already targeting React Native)
  - Targeting a single architecture.
  - A generic ABI, not specific to the library.
-->

---

- Why not? We don't need it

---

# Status quo

<v-clicks>

- You can extend React Native natively with TurboModules
  - Written in C++ / (Java | Kotlin) / (Objective-C | Swift)
- Write API prototype (the spec) in TypeScript
  - C++ / Java / Objective-C bindings are generated
  - Bridging between TypeScript and Native types is generated

</v-clicks>

---

# Status quo

```typescript
import { type TurboModule, TurboModuleRegistry } from 'react-native';

export interface Spec extends TurboModule {
  setItem(value: string, key: string): void;
  getItem(key: string): string | null;
  removeItem(key: string): void;
  clear(): void;
}

export default TurboModuleRegistry.getEnforcing<Spec>(
  'NativeLocalStorage',
);
```

---

# The shortcomings

<v-clicks>

- Does not cover the Web
- External libraries' build system needs to be integrated
    - Gradle/CMake for Android
    - Cocoapods for iOS
- Gets complicated quickly when using other languages
- JS API needs to be exported manually

</v-clicks>

---

# The solution

<v-clicks>

- The only performant way to run native code in the Browser
- Platform and architecture agnostic
  - Build artifacts can be used directly (no need to build from source!)
- Designed for performance and security
</v-clicks>