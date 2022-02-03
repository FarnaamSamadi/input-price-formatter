<script setup>
import { ref, watchEffect } from 'vue'
import InputPriceFormatter from '@/components/InputPriceFormatter.vue'

const price = ref('')

// auto focus on input
const priceInput = ref()
watchEffect(() => {
  if (priceInput.value) {
    priceInput.value.$el.focus()
  }
})
</script>

<template>
  <div id="app">
    <InputPriceFormatter
      v-model="price"
      label="مبلغ"
      has-rial
      ref="priceInput"
    />
  </div>
</template>

<style>
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

@font-face {
  font-family: 'IranSans';
  src: url(./assets/fonts/iransans.ttf) format('truetype');
}

#app {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 30px;
  background-color: #eee;
  font-family: 'IranSans', sans-serif;
}
</style>
