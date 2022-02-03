<script>
export default {
  name: 'InputPriceFormatter',

  emits: ['update:modelValue'],

  props: {
    modelValue: {
      type: [Number, String],
      default: ''
    }
  },

  setup(props) {
    return { props }
  }
}
</script>

<template>
  <div class="input"></div>
</template>

<style lang="scss" scoped></style>
