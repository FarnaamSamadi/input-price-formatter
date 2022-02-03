<script setup>
import { ref } from 'vue'
import InputPriceFormatter from '@/components/InputPriceFormatter.vue'

const price = ref(0)
</script>

<template>
  <div id="app">
    <InputPriceFormatter v-model="price" />
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

#app {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 30px;
  background-color: #eee;
}
</style>
