<script>
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  props: {
    title: String
  },

  setup() {

  },
})
</script>

<template>
  <input class="input" type="text">
</template>

<style scoped>
.input {
  font-size: 1.5rem;
}
</style>

