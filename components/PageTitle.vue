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
  <h1 class="title">{{ title }}</h1>
</template>

<style scoped>
.title {
  font-size: 1.5rem;
  text-align: center;
  font-weight: normal;
}
</style>

