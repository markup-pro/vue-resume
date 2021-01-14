<template>
  <div>
    <form @submit.prevent="formSubmit">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="type">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div :class="['form-control', { 'invalid': errors.name }]">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model.trim="value"></textarea>
        <small class="error" v-if="errors.name">{{ errors.name }}</small>
      </div>

      <app-btn color="primary" :is-disabled="disabledBtn" :loader="loader">Добавить</app-btn>
    </form>
  </div>
</template>

<script>
import AppBtn from '@/AppBtn'

export default {
  emits: {
    addResumeParams (data) {
      if (!data) {
        console.warn('No data in open-resume-params emit')
      } else if (Object.keys(data).length === 0) {
        console.warn('Data empty in open-resume-params emit')
      } else {
        return true
      }
    }
  },
  props: {
    loader: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      type: 'title',
      value: '',
      errors: {
        name: null
      }
    }
  },
  computed: {
    disabledBtn () {
      return this.value.length < 4
    }
  },
  methods: {
    formIsValid () {
      const regImg = (/\.(gif|jpe?g|png|webp|svg)$/i)
      let isValid = true

      if (this.value.length < 4) {
        this.errors.name = 'Поле должно содержать минимум 3 символа'
        isValid = false
      } else if (this.type === 'avatar' && !regImg.test(this.value)) {
        this.errors.name = 'Добавьте ссылку на изображение'
        isValid = false
      } else {
        this.errors.name = null
      }

      return isValid
    },
    formSubmit () {
      if (this.formIsValid()) {
        const formData = {
          type: this.type,
          value: this.value
        }
        this.$emit('addResumeParams', formData)
        this.type = 'title'
        this.value = ''
      }
    }
  },
  components: { AppBtn }
}
</script>
