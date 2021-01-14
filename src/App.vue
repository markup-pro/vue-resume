<template lang="html">
  <app-alert :text="alertText"></app-alert>

  <div class="container column">
    <div class="card card-w30">
      <resume-form
        :loader="loadForm"
        @add-resume-params="setResumeParams"
      ></resume-form>
    </div>
    <div class="card card-w70">
      <resume :data="resumeData"></resume>
    </div>
  </div>
  <div class="container">
    <app-comments
      :comments="commentsList"
      :loader="loadComments"
      @load-comments="getComments"
    ></app-comments>
  </div>
</template>

<script>
import AppAlert from '@/AppAlert'
import Resume from '@/components/Resume'
import ResumeForm from '@/components/ResumeForm'
import AppComments from '@/AppComments'

export default {
  data () {
    return {
      resumeData: [],
      commentsList: [],
      loadComments: false,
      loadForm: false,
      alertText: '',
      urlFirebase: process.env.VUE_APP_URL_FIREBASE,
      urlJsonPlaceholder: process.env.VUE_APP_URL_JSON
    }
  },
  mounted () {
    this.getDataResume()
  },
  methods: {
    hideAlert () {
      setTimeout(() => {
        this.alertText = ''
      }, 3000)
    },
    async getDataResume () {
      if (!this.loadForm) {
        try {
          const response = await fetch(`${this.urlFirebase}/resume.json`, {
            method: 'GET',
            headers: {
              'Content-Type': 'application-json'
            }
          })

          const data = await response.json()
          this.resumeData = Object.keys(data).map(key => {
            return {
              id: key,
              type: data[key].type,
              value: data[key].value
            }
          })
          this.alertText = 'Резюме успешно загружено'
          this.hideAlert()
        } catch (err) {
          console.error(err.message)
        }
      }
    },
    async setResumeParams (data) {
      if (!this.loadForm) {
        try {
          this.loadForm = true
          const response = await fetch(`${this.urlFirebase}/resume.json`, {
            method: 'POST',
            headers: {
              'Content-Type': 'application-json'
            },
            body: JSON.stringify(data)
          })

          this.resumeData.push({
            id: await response.json(),
            ...data
          })
          this.loadForm = false
          this.alertText = 'Резюме обновлено'
          this.hideAlert()
        } catch (err) {
          console.error(err.message)
        }
      }
    },
    async getComments () {
      try {
        if (!this.loadComments) {
          this.loadComments = true
          const response = await fetch(`${this.urlJsonPlaceholder}/comments?_limit=42`, {
            method: 'GET',
            headers: {
              'Content-Type': 'application-json'
            }
          })

          this.commentsList = await response.json()
          this.loadComments = false
          this.alertText = 'Комментарии успешно загружены'
          this.hideAlert()
        }
      } catch (err) {
        console.error(err.message)
      }
    }
  },
  components: { Resume, ResumeForm, AppComments, AppAlert }
}
</script>
