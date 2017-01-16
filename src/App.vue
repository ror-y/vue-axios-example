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
      data: [],
      errorMsg: 'No user or no location!'
    }
  },

  methods: {
    search() {
      const api = `https://api.github.com/users/${this.username}`
      var that = this 
      Vue.axios.get(api).then((response) => {        
        this.data = response.data
        console.log('user does not exist comes here')
      }).catch(error => {
        this.data = []
        console.log('user does not exist')
      })
    }
  }
}
</script>