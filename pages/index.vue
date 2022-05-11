<script setup lang="ts">
const title = 'コスパ計算'
const description = '量と金額を入力してどれがお得か計算します。'

useHead({
  meta: [{ name: 'description', content: description }],
  // link: [{ rel: 'stylesheet', href: './style.css' }],
  // script: [{ src: './script.js' }],
})

let count = ref<number>(2)
let beforeCount = ref<number>(2)
let priceArray = ref<number[]>([])
let amountArray = ref<number[]>([])
let pricePerAmount = ref<number[]>([])

const addElement = () => {
  beforeCount.value = count.value
  count.value++
}

const removeElement = (index) => {
  beforeCount.value = count.value
  count.value -= 1
  priceArray.value.splice(index, 1)
  amountArray.value.splice(index, 1)
  pricePerAmount.value.splice(index, 1)
}

const resetElement = () => {
  count.value = 0
  priceArray.value = []
  amountArray.value = []
  pricePerAmount.value = []
}

onMounted(() => {
  const item = document.querySelector('.item')
  item.querySelector('input').focus()
})

onUpdated(() => {
  if (beforeCount.value < count.value) {
    const item = document.querySelectorAll('.item')
    const last = item.length - 1
    item[last].querySelector('input').focus()
  }
})

const getUnitPrice = (index) => {
  const price = priceArray.value[index]
  const amount = amountArray.value[index]
  const existsValue = price > 0 && amount > 0

  if (existsValue) {
    const value =
      Math.round((priceArray.value[index] / amountArray.value[index]) * 10) / 10
    pricePerAmount.value[index] = value
  }
}

const costPosition = () => {
  const price = pricePerAmount.value
  if (price.length < 2) {
    return
  }

  const minValue = Math.min(...price)
  return price.indexOf(minValue)
}
</script>

<template>
  <div>
    <Title>{{ title }}</Title>
    <p v-if="costPosition() >= 0">{{ costPosition() + 1 }}がお得！！</p>
    <p v-else>金額と量を入力してください</p>
    <div class="list">
      <div
        class="item"
        :class="{ isActive: costPosition() === index }"
        v-for="(item, index) in count"
        :key="item"
      >
        {{ index + 1 }}
        <Input
          :value="priceArray[index]"
          v-model="priceArray[index]"
          @input="getUnitPrice(index)"
        />
        <Input
          :value="amountArray[index]"
          v-model="amountArray[index]"
          @input="getUnitPrice(index)"
        />
        <ButtonRemove @click="removeElement(index)" />
        <p v-if="pricePerAmount[index] > 0">@{{ pricePerAmount[index] }}円</p>
      </div>
    </div>

    <ButtonAdd @click="addElement" />
    <ButtonReset @click="resetElement" />
  </div>
</template>

<style scoped>
.isActive {
  border: 1px solid red;
}
</style>
