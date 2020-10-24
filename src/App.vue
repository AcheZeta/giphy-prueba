<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <div ></div>
    <!-- Search -->
    <input type="text" name="keyword" v-model="query" @keydown="getGifs"
    class="border py-2 px-5 text-grey-darkest shadow-inner">
    <!-- Trending -->
    <div v-for="gif in gifdata" :key="gif.id">
      <img :src="gif.images.original.url" :alt="gif.title">
    </div>
    <router-view/>
  </div>
</template>

<script>
// const axios = require('axios');
export default {
  name: 'App',
  data() {
    return {
      key: process.env.VUE_APP_APIKEY,
      url: process.env.VUE_APP_APIURL,
      query: '',
      gifdata: null,
    };
  },
  // beforeMount() {
  //   this.getGifs();
  // },
  mounted() {},
  methods: {
    getGifs() {
      const url = `${this.url}api_key=${this.key}&q=${this.query}&limit=4`;
      fetch(url)
        .then((response) => response.json())
        // eslint-disable-next-line no-return-assign
        .then((data) => this.gifdata = data.data);
    },
  },
};
</script>

<style >
@import "css/tailwind.css";

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
