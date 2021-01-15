<template>
  <button
    :class="['btn', color]"
    @click="$emit('action')"
    :disabled="isDisabled">
    <slot></slot>
    <span v-if="loader" class="btn__loader loader"></span>
  </button>
</template>

<script>
export default {
  name: 'AppBtn',
  emits: ['action'],
  props: {
    loader: {
      type: Boolean,
      default: false
    },
    color: {
      type: String,
      default: ''
    },
    isDisabled: {
      type: Boolean,
      default: false
    }
  }
}
</script>
