---
layout: section
transition: null
---

# Why WASM in React Native?

<!--
Robert for 5 minutes.
-->

---
layout: section
transition: null
---

# Truly universal apps

<v-click>

## React Universe

</v-click>

<!--
Our goal? To create truly universal apps.

[click] We at Callstack love React, and we have this goal,
we call React Universe, where you can use React to create truly
universal apps on any platform.
-->

---

# How to achieve this?

<div style="display: flex; flex: 1; gap: 40px; flex-direction: row; justify-content: center; margin-top: 150px;">

<v-click><img src="../react-logo.png" width="180" /></v-click>
<v-click><span style="font-size: 140px; color: white;">+</span></v-click>
<v-click><img src="../wa-logo.png" width="180" /></v-click>
</div>

<!--
So how can we achieve this? One of the ways is to embrace the WebAssembly,
and its growing ecosystem.
-->

---

# The environment

<div style="display: flex; flex: 1; gap: 40px; flex-direction: column; align-items: center; margin-top: 50px;">
<v-click>
<img src="../nodejs-logo.png" width="240" />
</v-click>

<div style="display: flex; gap: 40px; flex-direction: row; align-items: center; margin-top: 40px;">

<v-click>
<img src="../bun-logo.png" width="150" />
</v-click>

<v-click>
<img src="../deno-logo.png" width="120" />
</v-click>

</div>
</div>

<!--

So where are we?

The cool part about JS, and also the worst part, is that there are multiple environments
your code can run in, which is hard for a package maintainer.

[click] There's the biggest player, the first of the runtimes - nodejs.
[click] You can also use one of the newer and cooler runtimes like Bun, wich is written in Zig,
[click] or deno, written in rust.

And also the browser, which is also a valid environment.
-->

---

# The ecosystem

<div style="display: flex; flex-direction: column; align-items: center; margin-top: 150px;">

<img src="../npm-logo.png" width="400" />

</div>

<!--

One thing that they have in common, and what is widely used, is the npm.
However, the packages are not guaranteed to run between the runtimes.
Most of them do, but not all. And let's not forget the browser.

So one of the issues is that packages can depend on WebAPIs, or NodeAPI. Neither of
which is supported by React Native currently.
-->

---

# Status quo

Extending React Native with native code

<v-clicks depth="2">

- You can extend React Native natively with TurboModules
  - Written in C++ / (Java | Kotlin) / (Objective-C | Swift)
  - Access JavaScript environment through the JSI
- Write API prototype (the spec) in TypeScript
  - C++ / Java / Objective-C bindings are generated
  - Bridging between TypeScript and Native types is generated

</v-clicks>

<!--
(1 min)

So how is it as of today?

[click]
You can already extend React Native with native functionalities using what's
called Turbo Modules 
[click]
These are written in either pure C++, or C++ with platform native code, such as Java or ObjC.
This is needed to access native UI components. 
[click]
You can access and extend the JavaScript environment through the JavaScript Interface,
which abstracts away various JS engines (JSC and Hermes).
[click]
Rather than writing it all by hand, we use a tool called codegen.
[click]
This reads the TypeScript (or Flow) spec and generates the bridging boilerplate code,
which is for you to implement.
[click]
Also, complex types are automatically bridged between TypeScript and native types.
-->

---

# Status quo

An example TurboModule Spec

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

<!--
This is a simple example of a LocalStorage module spec. This acts as a contract.
-->

---

# Status quo

Generated code

```cpp
class JSI_EXPORT NativeLocalStorageSpecCxxSpecJSI : public TurboModule {
protected:
  NativeLocalStorageSpecCxxSpecJSI(std::shared_ptr<CallInvoker> jsInvoker);

public:
  virtual void setItem(jsi::Runtime &rt, jsi::String value, jsi::String key) = 0;
  virtual std::optional<jsi::String> getItem(jsi::Runtime &rt, jsi::String key) = 0;
  virtual void removeItem(jsi::Runtime &rt, jsi::String key) = 0;
  virtual void clear(jsi::Runtime &rt) = 0;
};

// ...
// much more core below
// ...
```

<!-- 
The generated code looks more or less like this. 
There is more code which is not really important to us right now.

What we should do next, is to extend this class and implement the methods.
-->

---

# The shortcomings of TurboModules

<v-clicks depth="2">

- Does not cover the Web
- External libraries' build system needs to be integrated
    - Gradle/CMake for Android
    - Cocoapods for iOS
- Gets complicated quickly when using other languages
- You need to expose JS functions manually (writing the Spec)

</v-clicks>

<!--

[click] One of the biggest shortcomings is that this approach does not cover the Web.
[click] When integrating external libraries, you need to integrate their build system.
[click] For android, this is Gradle with CMake, [click] for iOS it's Cocoapods.

[click] This approach is not so straightforward when trying to integrate, say, rust library.

[click] When trying to expose native library to JS, you need to write the spec, expose the library functions
manually. And on top of that, you need to maintain it.

-->

---

# The solution

<v-click>WebAssembly 💙</v-click>

<v-clicks depth="2">

- The go-to solution to run native code in the Browser
- Platform and architecture agnostic
  - Build artifacts can be used directly (no need to build from source!)
- Designed for performance and security

</v-clicks>

<!-- 

[click]
[click] Using WebAssembly really bridges all gaps we've just talked about.
[click] Since the modules are sandboxed, there's no need to worry about triplets, platforms and such
[click]There's no issues and headaches with integrating build systems. 
You just consume the prebuilds of other libraries.

[click] The modules are sandboxed, and see only as much as we give them access to.
-->