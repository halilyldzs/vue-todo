<template>
  <div class="max-w-2xl mx-auto p-4">
    <h1 class="text-3xl font-bold text-center mb-8">Todo App</h1>

    <TodoInput @add-todo="addTodo" />

    <TodoFilter
      :filter="currentFilter"
      :has-completed="hasCompletedTodos"
      @filter-change="currentFilter = $event"
      @clear-completed="clearCompleted"
    />

    <TransitionGroup name="list" class="flex flex-col">
      <TodoItem
        v-for="todo in filteredTodos"
        :key="todo.id"
        :todo="todo"
        @toggle="toggleTodo"
        @delete="deleteTodo"
      />
    </TransitionGroup>

    <div v-if="todos.length === 0" class="text-center text-gray-500 mt-8">
      No todos yet. Add one above!
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import TodoInput from '@/components/TodoInput.vue'
import TodoItem from '@/components/TodoItem.vue'
import TodoFilter from '@/components/TodoFilter.vue'

interface Todo {
  id: number
  text: string
  completed: boolean
}

const todos = ref<Todo[]>([])
const currentFilter = ref<'all' | 'active' | 'completed'>('all')
let nextId = 1

const hasCompletedTodos = computed(() => todos.value.some((todo) => todo.completed))

const filteredTodos = computed(() => {
  switch (currentFilter.value) {
    case 'active':
      return todos.value.filter((todo) => !todo.completed)
    case 'completed':
      return todos.value.filter((todo) => todo.completed)
    default:
      return todos.value
  }
})

const addTodo = (text: string) => {
  todos.value.push({
    id: nextId++,
    text,
    completed: false,
  })
}

const toggleTodo = (id: number) => {
  const todo = todos.value.find((t) => t.id === id)
  if (todo) {
    todo.completed = !todo.completed
  }
}

const deleteTodo = (id: number) => {
  const index = todos.value.findIndex((t) => t.id === id)
  if (index !== -1) {
    todos.value.splice(index, 1)
  }
}

const clearCompleted = () => {
  todos.value = todos.value.filter((todo) => !todo.completed)
}
</script>

<style>
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list-leave-active {
  position: absolute;
}
</style>
