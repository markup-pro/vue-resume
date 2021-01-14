<template>
  <h2>{{ data.value }}</h2>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
      default: () => {
        return {}
      },
      validator (value) {
        return Object.keys(value).length !== 0
      }
    }
  }
}
</script>
