<template>
  <div id="app">
    <form @submit.prevent="search">
      <input v-model="username" placeholder="Enter a github user!" />
    </form>
    <p v-if="data.name">
      {{ data.name }} ({{ data.login }})
      is from
      {{ data.location }}!
    </p>
    <p v-else>{{ errorMsg }}</p>
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
 
Vue.use(VueAxios, axios)

export default {
  data() {
    return {
      username: '',
      data: []
    }
  },

  methods: {
    search() {
      const api = `https://api.github.com/users/${this.username}`

      Vue.axios.get(api).then((response) => {        
        this.data = response.data
      }).catch(error => {
        this.errorMsg = 'No user or no location!'
        this.data = []
      })

    }
  }
}
</script>