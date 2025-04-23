<template>
  <div class="flex gap-2 mb-4">
    <InputText
      v-model="newTodo"
      placeholder="Add new todo..."
      class="flex-1 p-2"
      @keyup.enter="addTodo"
    />
    <Button icon="pi pi-plus" severity="success" @click="addTodo" :disabled="!newTodo.trim()" />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import InputText from 'primevue/inputtext'
import Button from 'primevue/button'

const newTodo = ref('')

const emit = defineEmits<{
  (e: 'add-todo', value: string): void
}>()

const addTodo = () => {
  const todoText = newTodo.value.trim()
  if (todoText) {
    emit('add-todo', todoText)
    newTodo.value = ''
  }
}
</script>
