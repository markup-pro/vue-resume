<template>
  <div class="card">
    <h2>Комментарии</h2>
    <ul class="list" v-if="comments.length !== 0">
      <li
        class="list-item"
        v-for="comment in comments"
        :key="comment.id">
        <div>
          <p><strong>{{ comment.email }}</strong></p>
          <small>{{ comment.name }}</small>
        </div>
      </li>
    </ul>
    <p v-else>Пока нет комментариев</p>
    <p v-if="comments.length === 0">
      <app-btn
        class="primary"
        @action="$emit('loadComments')"
        :loader="loader">Загрузить комментарии</app-btn>
    </p>
  </div>
</template>

<script>
import AppBtn from '@/AppBtn'

export default {
  emits: ['loadComments'],
  props: {
    comments: {
      type: Array,
      required: true,
      default: function () {
        return []
      }
    },
    loader: {
      type: Boolean,
      default: false
    }
  },
  components: { AppBtn }
}
</script>
