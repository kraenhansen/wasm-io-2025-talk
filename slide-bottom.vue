<template>
  <footer class="absolute bottom-0 left-0 right-0 p-3 text-center text-sm opacity-50">
    <div v-if="$nav.currentLayout !== 'image-left' && $nav.currentLayout !== 'image-right'">
      <code>@kraenhansen.dk</code> / <code>@rpasinski.pl</code> on Bluesky 🦋
    </div>
    <div v-if="$nav.currentLayout !== 'image-left' && $nav.currentLayout !== 'image-right' && $nav.currentLayout !== 'intro'" class="absolute top-0 bottom-0 right-0 p-1 flex items-center">
      <img src="./callstack-shortlogo.svg" style="height:1.5rem;margin:0 0.5rem;" />
      ⤫
      <img src="./mongodb-logomark.svg" style="height:1.5rem;margin:0 0.5rem;" />
    </div>
  </footer>
</template>
