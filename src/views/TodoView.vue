<script setup>
import TodoList from '@/components/TodoList.vue'
import { ref, watch, onBeforeMount } from 'vue'
import { uid } from 'uid'
const todo = ref('')
const todos = ref([])
let archive = localStorage.getItem('todos')

watch(
  todos,
  () => {
    localStorage.setItem('todos', JSON.stringify(todos.value))
  },
  { deep: true },
)

onBeforeMount(() => {
  // The key 'todos' exists but its value is not empty.
  if (archive !== '' && archive !== null) {
    todos.value = JSON.parse(archive)
  }
})

const addTodo = () => {
  if (todo.value != '') {
    todos.value.push({
      id: uid(),
      text: todo.value,
      isComplete: false,
      isEditing: false,
    })
  }
  todo.value = ''
}

const handleCheckbox = (index) => {
  todos.value[index].isComplete = !todos.value[index].isComplete
}
const handleDelete = (index) => {
  todos.value.splice(index, 1) // Remove the item at the specified index
}
const handleEdit = (index) => {
  todos.value[index].isEditing = !todos.value[index].isEditing
}
const handleUpdate = (index, text) => {
  todos.value[index].isEditing = !todos.value[index].isEditing
  todos.value[index].text = text
}
</script>

<template>
  <h2>Create Todo</h2>
  <!-- Create Todo -->
  <div class="flex rounded-lg shadow-sm">
    <input
      v-model="todo"
      type="text"
      id="hs-trailing-button-add-on"
      name="hs-trailing-button-add-on"
      class="py-3 px-4 block w-full border-gray-200 shadow-sm rounded-s-lg text-sm focus:z-10 focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none dark:bg-neutral-900 dark:border-neutral-700 dark:text-neutral-400 dark:placeholder-neutral-500 dark:focus:ring-neutral-600"
    />
    <button
      @click="addTodo"
      type="button"
      class="py-3 px-4 inline-flex justify-center items-center gap-x-2 text-sm font-semibold rounded-e-md border border-transparent bg-blue-600 text-white hover:bg-blue-700 focus:outline-none focus:bg-blue-700 disabled:opacity-50 disabled:pointer-events-none"
    >
      Create
    </button>
  </div>
  <!-- Show Todo -->
  <div>
    <ul class="w-96 flex flex-col">
      <TodoList
        @todo-update="handleUpdate"
        @todo-edit="handleEdit"
        @todo-delete="handleDelete"
        @todo-checkbox="handleCheckbox"
        v-for="(todo, index) in todos"
        :index="index"
        :todo="todo"
        :key="todo.id"
      />
    </ul>
  </div>
</template>
