<template>
  <div v-if="data.length === 0">Добавьте данные в резюме</div>
  <div v-else>
    <component
      v-for="item in data"
      :is="`app-${item.type}`"
      :key="item.id"
      :data="item"></component>
  </div>
</template>

<script>
import AppTitle from '@/AppTitle'
import AppSubtitle from '@/AppSubtitle'
import AppAvatar from '@/AppAvatar'
import AppText from '@/AppText'

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
  components: { AppTitle, AppSubtitle, AppAvatar, AppText }
}
</script>
