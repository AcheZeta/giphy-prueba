<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <div v-for="gif in gifdata" :key="gif.id">
      <img :src="gif.images.original.url" :alt="gif.title">
    </div>
    <router-view/>
  </div>
</template>

<script>
const axios = require('axios');

export default {
  name: 'App',
  data() {
    return {
      key: process.env.VUE_APP_APIKEY,
      url: process.env.VUE_APP_APIURL,
      keyword: 'Star Wars',
      gifdata: null,
    };
  },
  beforeMount() {
    this.getName();
  },
  mounted() {},
  methods: {
    async getName() {
      const { data } = await axios.get(`${this.url}api_key=${this.key}`);
      this.gifdata = data.data;
      // eslint-disable-next-line no-console
      console.log(this.gifdata.data);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
