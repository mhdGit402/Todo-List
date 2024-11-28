<script setup>
import { ref } from 'vue'
defineEmits(['todo-checkbox', 'todo-delete', 'todo-edit', 'todo-update'])
// Define props directly
const { todo, index } = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
})

let updatedText = ref(todo.text)
</script>

<template>
  <li
    class="inline-flex items-center gap-x-2 py-3 px-4 text-sm font-semibold bg-white border border-gray-300 text-gray-900 -mt-px first:rounded-t-lg first:mt-0 last:rounded-b-lg"
  >
    <div>
      <input
        @input="$emit('todo-checkbox', index)"
        :checked="todo.isComplete"
        id="default-checkbox"
        type="checkbox"
        class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
      />
    </div>
    <div class="group flex justify-between w-full">
      <input
        v-if="todo.isEditing"
        v-model="updatedText"
        type="text"
        id="hs-trailing-button-add-on"
        name="hs-trailing-button-add-on"
        class="py-3 px-4 block w-full border-gray-200 shadow-sm rounded-s-lg text-sm focus:z-10 focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none dark:bg-neutral-900 dark:border-neutral-700 dark:text-neutral-400 dark:placeholder-neutral-500 dark:focus:ring-neutral-600"
      />
      <span :class="[todo.isComplete ? 'completed' : '']" v-else> {{ todo.text }} </span>
      <button
        v-if="!todo.isEditing"
        @click="$emit('todo-edit', index)"
        class="inline-flex items-center py-1 px-2 rounded-full text-xs font-semibold transition-all duration-150 bg-gray-300 text-gray-700 hover:bg-[#41b883] hover:text-white"
      >
        Edit
      </button>
      <button
        v-else
        @click="$emit('todo-update', index, updatedText)"
        class="inline-flex items-center py-1 px-2 rounded-full text-xs font-semibold transition-all duration-150 bg-gray-300 text-gray-700 hover:bg-blue-500 hover:text-white"
      >
        Update
      </button>
      <button
        @click="$emit('todo-delete', index)"
        class="inline-flex items-center py-1 px-2 rounded-full text-xs font-semibold transition-all duration-150 bg-gray-300 text-gray-700 hover:bg-[#f87171] hover:text-white"
      >
        Delete
      </button>
    </div>
  </li>
</template>

<style>
.completed {
  text-decoration: line-through;
}
</style>
