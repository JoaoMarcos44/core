<script setup>
const { message } = defineProps({ message: { default: 'prop' } })
function caught() {
  try { throw { message: 'caught' } }
  catch ({ message }) { return message }
}
function switched() {
  switch (0) {
    case 0:
      const message = 'case'
      return message
  }
}
</script>
<template>
  <p>catch: {{ caught() }}</p>
  <p>switch: {{ switched() }}</p>
</template>

