<template>
  <h2>{{ data.value }}</h2>
</template>

<script>
export default {
  name: 'ResumeViewSubtitle',
  props: {
    data: {
      type: Object,
      required: true,
      default: () => {
        return {}
      },
      validator (value) {
        return !!Object.keys(value).length
      }
    }
  }
}
</script>
