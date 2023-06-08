<script lang="ts" setup>
useHead({
  title: "Pesilat",
  meta: [{ name: "description", content: "My amazing site." }],
  bodyAttrs: {
    class: "test",
  },
  script: [{ innerHTML: "console.log('Hello world')" }],
});
</script>

<template>
  <Header />

  <div class="xl:w-3/5 lg:w-3/4 sm:w-5/6 h-fit mx-auto mt-2">
    <slot />
  </div>
</template>
