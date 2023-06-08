<script lang="ts" setup>
useHead({
  title: "Pesilat | Home",
  meta: [{ name: "description", content: "My amazing site." }],
  bodyAttrs: {
    class: "test",
  },
  script: [{ innerHTML: "console.log('Hello world')" }],
});
</script>

<template>
  <div class="flex justify-center items-center flex-col">
    <h1 class="text-4xl">Lorem Ipsum This is Home Page</h1>
    <div class="mt-2">
      <h2 class="text-3xl text-red-500">
        Click the button below to be directed to the To-Do List page.
      </h2>
    </div>
    <div class="mt-5">
      <NuxtLink
        to="/to-do"
        class="rounded-full bg-blue-500 px-5 py-3 font-semibold text-white"
        >To Do List</NuxtLink
      >
    </div>
  </div>
</template>
