<template>
  <div v-if="data.length === 0">Добавьте данные в резюме</div>
  <div v-else>
    <component
      v-for="item in data"
      :is="`resume-${item.type}`"
      :key="item.id"
      :data="item"></component>
  </div>
</template>

<script>
import ResumeTitle from '@/components/ResumeTitle'
import ResumeSubtitle from '@/components/ResumeSubtitle'
import ResumeAvatar from '@/components/ResumeAvatar'
import ResumeText from '@/components/ResumeText'

export default {
  props: {
    data: {
      type: Array,
      required: true,
      default: function () {
        return []
      }
    }
  },
  components: { ResumeTitle, ResumeSubtitle, ResumeAvatar, ResumeText }
}
</script>
