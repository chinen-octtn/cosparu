<script setup lang="ts"></script>

<template>
  <input
    class="input"
    type="text"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<style scoped>
.input {
  font-size: 1.5rem;
  border: 1px solid #000;
}
</style>
