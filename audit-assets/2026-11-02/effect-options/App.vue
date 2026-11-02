<script setup>
import { effect, ref, stop } from 'vue'

let schedulerCalls = 0
let onStopCalls = 0
let secondRuns = 0
const options = {
  scheduler: () => schedulerCalls++,
  onStop: () => onStopCalls++,
}

const firstSource = ref(0)
const secondSource = ref(0)
const first = effect(() => firstSource.value, options)
const second = effect(() => {
  secondRuns++
  return secondSource.value
}, options)

firstSource.value++
secondSource.value++
stop(first)
stop(second)

let frozenError = 'none'
try {
  const runner = effect(() => {}, Object.freeze({ onStop: () => {} }))
  stop(runner)
} catch (error) {
  frozenError = `${error.name}: ${error.message}`
}

const result = { schedulerCalls, onStopCalls, secondRuns, frozenError }
</script>

<template>
  <pre id="result">{{ JSON.stringify(result, null, 2) }}</pre>
</template>

