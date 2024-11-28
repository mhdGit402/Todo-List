<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header
    class="flex flex-wrap sm:justify-start sm:flex-nowrap w-full bg-white text-sm py-3 dark:bg-neutral-800"
  >
    <nav class="max-w-[85rem] w-full mx-auto px-4 sm:flex sm:items-center sm:justify-between">
      <span
        class="flex-none font-semibold text-xl text-black focus:outline-none focus:opacity-80 dark:text-white"
        aria-label="Brand"
        >Todo List App</span
      >
      <div class="flex flex-row items-center gap-5 mt-5 sm:justify-end sm:mt-0 sm:ps-5">
        <RouterLink
          :to="{ name: 'todo' }"
          class="font-medium text-blue-500 focus:outline-none"
          aria-current="page"
          >Home</RouterLink
        >
        <RouterLink
          :to="{ name: 'about' }"
          class="font-medium text-gray-600 hover:text-gray-400 focus:outline-none focus:text-gray-400 dark:text-neutral-400 dark:hover:text-neutral-500 dark:focus:text-neutral-500"
          >About</RouterLink
        >
      </div>
    </nav>
  </header>
</template>
