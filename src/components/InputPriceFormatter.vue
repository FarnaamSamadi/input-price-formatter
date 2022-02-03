<script>
import { ref, toRef, computed } from 'vue'

export default {
  name: 'InputPriceFormatter',

  emits: ['update:modelValue'],

  props: {
    modelValue: {
      type: [Number, String],
      default: ''
    },
    hasRial: {
      type: Boolean,
      default: false
    },
    label: {
      type: String,
      default: ''
    }
  },

  setup(props, { emit }) {
    const isFocused = ref(false)
    const hiddenInput = ref()

    const handleFocus = () => {
      isFocused.value = true
      hiddenInput.value.focus()
    }

    const handleBlur = () => {
      isFocused.value = false
    }

    const updateValue = ($event) => {
      const output = $event.target.value.substr(0, 16).replace(/[^0-9]/g, '')
      $event.target.value = output
      emit('update:modelValue', output)
    }

    const inputValue = toRef(props, 'modelValue')
    const inputToShow = computed(() => {
      const inputStd = inputValue.value.substr(0, 15)
      return inputStd.length > 0 ? parseInt(inputStd).toLocaleString() : ''
    })

    const showLabel = computed(() => {
      return !(inputValue.value.length > 0 || isFocused.value)
    })

    return {
      isFocused,
      updateValue,
      handleFocus,
      hiddenInput,
      handleBlur,
      showLabel,
      inputToShow
    }
  }
}
</script>

<template>
  <div class="input" tabindex="0" @focus="handleFocus">
    <div class="input__inner">
      <div class="input__row">
        <span class="input__rial" v-if="hasRial">ریال</span>
        <p :class="['input__text', isFocused && 'input__text--focused']">
          {{ inputToShow }}
        </p>
      </div>
      <label v-if="showLabel" class="input__label">
        {{ label }}
      </label>
      <i :class="['input__line', isFocused && 'input__line--focused']" />
    </div>

    <input
      ref="hiddenInput"
      autocomplete="off"
      class="input__input"
      type="number"
      :value="modelValue"
      @input="updateValue"
      @blur="handleBlur"
    />
  </div>
</template>

<style lang="scss" scoped>
.input {
  width: 400px;
  height: 40px;
  padding: 0;
  margin: 0;
  outline: none;
  cursor: text;

  &__inner {
    position: relative;
    width: 100%;
    height: 100%;
  }

  &__row {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    left: 0;
    top: 0;
    bottom: 0;
    direction: ltr;
  }

  &__input {
    text-align: left;
    direction: ltr;
    opacity: 0;
    width: 100%;
  }

  &__line {
    height: 1px;
    width: 100%;
    position: absolute;
    bottom: 0;
    right: 0;
    left: 0;
    background-color: #000;
    transition: all 0.3s ease;

    &--focused {
      background-color: #06ad0e;
    }
  }

  &__text {
    display: inline-block;
    min-width: 2px;
    height: 40px;
    text-align: left;
    font-size: 25px;
    padding: 2px 0 0;
    color: #111;

    &--focused {
      border-right: 1px solid #111;
      animation: cursorBlink 1s infinite;
    }
  }

  &__rial {
    display: inline-block;
    font-size: 15px;
    color: #555;
    margin-right: 10px;
  }

  &__label {
    position: absolute;
    top: 9px;
    right: 4px;
    bottom: 0;
    font-size: 15px;
    color: #000;
    pointer-events: none;
    transition: all 0.5s ease;
  }
}

@keyframes cursorBlink {
  50% {
    border-right-color: #000;
  }
  51% {
    border-right-color: transparent;
  }
  100% {
    border-right-color: transparent;
  }
}
</style>
