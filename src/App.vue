<template>
  <div class="container column">
    <form-control @get-resume-field="getResumeField"/>
    <div class="card card-w70" v-if="resume.length !== 0">
      <component
        v-for="item in resume"
        :key="item"
        :is="`app-${item.type}`"
        :text="item.text"
      />
    </div>
  </div>
  <list-of-comments />
</template>

<script>
import FormControl from '@/components/FormControl.vue'
import ListOfComments from '@/components/ListOfComments.vue'
import AppTitle from '@/components/AppTitle.vue'
import AppSubtitle from '@/components/AppSubtitle.vue'
import AppAvatar from '@/components/AppAvatar.vue'
import AppText from '@/components/AppText.vue'
import axios from 'axios'
export default {
  components: {
    ListOfComments,
    AppAvatar,
    FormControl,
    AppTitle,
    AppSubtitle,
    AppText
  },
  data () {
    return {
      resume: []
    }
  },
  mounted () {
    this.loadResume()
  },
  methods: {
    async getResumeField (val) {
      await axios.post('https://vue-demo-deploy-5b615-default-rtdb.firebaseio.com/resume.json', {
        val
      })
        .then((response) => {
          this.resume.push({
            id: response.data.name,
            ...val
          })
        })
    },
    async loadResume () {
      await axios.get('https://vue-demo-deploy-5b615-default-rtdb.firebaseio.com/resume.json')
        .then((response) => {
          if (response.data) {
            this.resume = Object.keys(response.data).map(key => {
              return {
                id: key,
                ...response.data[key].val
              }
            })
          }
        })
        .catch((error) => {
          this.resume = []
          console.log(error)
        })
    }
  }
}
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
