<template>
  <transition name="fade">
    <div v-if="isShow" :class="['alert', color]">
      <div class="container">
        <small>{{ text }}</small>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      default: 'primary'
    },
    text: {
      type: String,
      required: true
    }
  },
  computed: {
    isShow () {
      return this.text
    }
  }
}
</script>

<style>
  .alert {
    position: fixed;
    top: 0;
    right: 15px;
    width: 320px;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s ease;
  }

  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }
</style>
