<template>
  <div class="avatar">
    <img :src="data.value">
  </div>
</template>

<script>
export default {
  name: 'ResumeViewAvatar',
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
