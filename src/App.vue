<template>
  <div id="app" class="h-24 bg-gradient-to-r from-purple-200 to-pink-400">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <main>
      <section id="search-section">
        <!-- Search -->
        <label for="gifsearch">Busca un Gif</label>
        <input
          id="gifsearch"
          type="text"
          name="keyword"
          v-model="query"
          @keydown="getGifs"
          class="border rounded-lg py-2 px-5 text-grey-darkest shadow-inner m-8"
          placeholder="cat"
        />
      </section>
      <!-- Trending -->
      <section
        class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-4"
      >
        <figure v-for="gif in gifdata" :key="gif.id" class="p-4">
          <img
            class="rounded-lg"
            :src="gif.images.original.url"
            :alt="gif.title"
          />
        </figure>
      </section>
    </main>
    <router-view />
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
      const url = `${this.url}api_key=${this.key}&q=${this.query}&limit=10`;
      fetch(url)
        .then((response) => response.json())
        // eslint-disable-next-line no-return-assign
        .then((data) => (this.gifdata = data.data));
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
