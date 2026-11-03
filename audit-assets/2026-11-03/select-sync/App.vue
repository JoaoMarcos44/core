<script setup>
import { computed, ref } from 'vue'

const selected = ref('alice')
const people = [
  { id: 'alice', name: 'Alice' },
  { id: 'bob', name: 'Bob' },
  { id: 'carol', name: 'Carol' },
]
const memberIds = ref(['alice'])

const members = computed(() =>
  people.filter(person => memberIds.value.includes(person.id)),
)
const others = computed(() =>
  people.filter(person => !memberIds.value.includes(person.id)),
)

function assign(event) {
  const id = event.target.value
  if (!memberIds.value.includes(id)) {
    memberIds.value = [...memberIds.value, id]
  }
}
</script>

<template>
  <h1>Assign a project member</h1>
  <p>Selecting a person immediately adds them to the project.</p>
  <p>Model (assignee id): <output id="model">{{ selected }}</output></p>
  <label>
    Assignee:
    <select id="choice" v-model="selected" @change="assign">
      <optgroup label="Project members">
        <option v-for="person in members" :key="person.id" :value="person.id">
          {{ person.name }}
        </option>
      </optgroup>
      <optgroup label="Other people">
        <option v-for="person in others" :key="person.id" :value="person.id">
          {{ person.name }}
        </option>
      </optgroup>
    </select>
  </label>
</template>
