<template>
  <div
    class="flex items-center gap-3 p-3 mb-2 rounded-lg border border-gray-200 hover:bg-gray-50 transition-colors"
    :class="{ 'bg-gray-50': todo.completed }"
  >
    <Checkbox
      :modelValue="todo.completed"
      :binary="true"
      @update:modelValue="$emit('toggle', todo.id)"
    />
    <span class="flex-1" :class="{ 'line-through text-gray-500': todo.completed }">
      {{ todo.text }}
    </span>
    <Button
      icon="pi pi-trash"
      severity="danger"
      text
      @click="$emit('delete', todo.id)"
      class="p-2"
    />
  </div>
</template>

<script setup lang="ts">
import Checkbox from 'primevue/checkbox'
import Button from 'primevue/button'

interface Todo {
  id: number
  text: string
  completed: boolean
}

defineProps<{
  todo: Todo
}>()

defineEmits<{
  (e: 'toggle', id: number): void
  (e: 'delete', id: number): void
}>()
</script>
