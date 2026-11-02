<script setup>
import { ref } from 'vue'

const selected = ref('a')
const options = ref([
  { id: 1, value: 'a' },
  { id: 2, value: 'b' },
])

function refreshOptions() {
  options.value = [
    { id: 1, value: 'a' },
    { id: 3, value: 'b' },
  ]
}
</script>

<template>
  <p>Model: {{ selected }}</p>
  <select v-model="selected" @change="refreshOptions">
    <option v-for="option in options" :key="option.id" :value="option.value">
      {{ option.value }}
    </option>
  </select>
</template>

