<template>
  <div v-if="!data.length">Добавьте данные в резюме</div>
  <div v-else>
    <component
      v-for="item in data"
      :is="`resume-view-${item.type}`"
      :key="item.id"
      :data="item"></component>
  </div>
</template>

<script>
import ResumeViewTitle from '@/components/ResumeViewTitle'
import ResumeViewSubtitle from '@/components/ResumeViewSubtitle'
import ResumeViewAvatar from '@/components/ResumeViewAvatar'
import ResumeViewText from '@/components/ResumeViewText'

export default {
  name: 'ResumeView',
  props: {
    data: {
      type: Array,
      required: true,
      default: function () {
        return []
      }
    }
  },
  components: { ResumeViewTitle, ResumeViewSubtitle, ResumeViewAvatar, ResumeViewText }
}
</script>
