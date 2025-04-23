<template>
  <div class="flex justify-between items-center mb-4">
    <div class="flex gap-2">
      <Button
        :class="{ 'p-button-outlined': filter !== 'all' }"
        @click="$emit('filter-change', 'all')"
        label="All"
      />
      <Button
        :class="{ 'p-button-outlined': filter !== 'active' }"
        @click="$emit('filter-change', 'active')"
        label="Active"
      />
      <Button
        :class="{ 'p-button-outlined': filter !== 'completed' }"
        @click="$emit('filter-change', 'completed')"
        label="Completed"
      />
    </div>
    <Button
      v-if="hasCompleted"
      severity="danger"
      text
      @click="$emit('clear-completed')"
      label="Clear Completed"
    />
  </div>
</template>

<script setup lang="ts">
import Button from 'primevue/button'

defineProps<{
  filter: 'all' | 'active' | 'completed'
  hasCompleted: boolean
}>()

defineEmits<{
  (e: 'filter-change', filter: 'all' | 'active' | 'completed'): void
  (e: 'clear-completed'): void
}>()
</script>
