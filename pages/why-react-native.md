---
layout: section
transition: null
---

# React Native

<!--
(5 min)
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
-->

<!--
Kræn for 5 minutes:

I imagine most of the folks in this audience are already very familiar with WebAssembly
and less familiar with React Native.
-->

--- 

# React Native

<v-clicks at="0">

- Enables building cross-platform native apps
- Popular and widely adopted (> 3 mio weekly downloads on NPM)
- Large ecosystem of [> 1K actively maintained packages](https://reactnative.directory/?isMaintained=true)
- Stewarded by Meta
- Initially released 10 years ago

</v-clicks>

<img width="80%" src="../react-native-devices.png" class="m-a p-10" />

<!--
In it's essence, it's a tool-kit to enable building cross-platform native apps, written mainly in JavaScript / TypeScript, which run on
- iOS
- Android
- Desktop macOS / Windows
- and the web

[click] Popular and widely adopted (more than 3 million weekly downloads on NPM)
[click] Large ecosystem of more than 1000 actively maintained packages targeting React Native
[click] Stewarded by Meta
[click] Initially released 10 years ago (as of yesterday!)
-->

---

# React <span class="opacity-30">Native</span>

Built around the most used framework for building reactive UIs.

```tsx
import React, { useState } from 'react';


const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <span>Count: {count}</span>
      <button onPress={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

<!--
// Add a link to the state of javascript
-->

<!--
One part of React Native is React:
As it's built around the most popular framework for building reactive UIs.
-->

---

# <span class="opacity-30">React</span> Native

Expose native UI (iOS, Android, etc.) to apps written in JavaScript / TypeScript.

```tsx
import React, { useState } from 'react';
import { View, Text, Button } from 'react-native';

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <View>
      <Text>Count: {count}</Text>
      <Button title="Increment" onPress={() => setCount(count + 1)} />
    </View>
  );
};
```

<!--
The other part of "React Native" is Native:
The application UI are composed of the actual native views provided by the platform.
-->

---

# React Native

<v-clicks>

- Used JavaScriptCore previously, with message-passing between JavaScript and native
- Now uses the Hermes JavaScript engine (by default)
- Very limited runtime APIs

</v-clicks>

<!--
In the context of this talk, there's a few details I want to highlight:
[click] The default JavaScript engine for React Native apps is Hermes - a JavaScript Engine built by Meta for React Native. Focused on first-time-to-interactive.
[click] Hermes brings almost no runtime APIs and doesn't bring WebAssembly - in particular.
-->

