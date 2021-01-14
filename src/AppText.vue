<template>
  <p>{{ data.value }}</p>
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
