<template>
  <div id="app">
    <form @submit.prevent="search">
      <input v-model="username" />
    </form>
    <p v-if="data">
      {{ data.name }} ({{ data.login }})
      is from
      {{ data.location }}!
    </p>
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
        console.log(error)
      })
    }
  }
}
</script>