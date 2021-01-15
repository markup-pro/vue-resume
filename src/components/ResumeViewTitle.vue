<template>
  <h1>{{ data.value }}</h1>
</template>

<script>
export default {
  name: 'ResumeViewTitle',
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
