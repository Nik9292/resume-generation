<template>
  <div class="container">
    <p>
      <button class="btn primary" @click="loadListComments">Загрузить комментарии</button>
    </p>
    <div class="card" v-if="comments.length">
      <h2>Комментарии</h2>
      <ul class="list">
        <person-comment v-for="comment in comments" :comment="comment" :key="comment"/>
      </ul>
    </div>
    <app-loader v-if="loading"/>
  </div>
</template>

<script>
import PersonComment from '@/components/PersonComment.vue'
import AppLoader from '@/components/AppLoader.vue'
import axios from 'axios'
export default {
  components: {
    PersonComment,
    AppLoader
  },
  data () {
    return {
      comments: [],
      loading: false
    }
  },
  methods: {
    async loadListComments () {
      this.loading = true
      await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
        .then((response) => {
          this.comments = response.data
          this.loading = false
        })
        .catch((error) => {
          console.log(error)
          this.loading = false
        })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
