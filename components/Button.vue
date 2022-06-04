<script setup lang="ts">
const props = defineProps({
  text: String,
})
</script>

<template>
  <button type="button">{{ props.text }}</button>
</template>

<style scoped>
button {
  font-weight: normal;
  /* box-shadow: 0 0 3px rgba(0, 0, 0, 0.3); */
  border: none;
  appearance: none;
}
</style>
