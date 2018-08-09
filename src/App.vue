<template>
  <div id="app">
    <div>
  <b-nav>
    <b-nav-item>Nombre tienda</b-nav-item>
    <b-nav-item><router-link :to="{ name: 'HelloWorld' }">Home</router-link></b-nav-item>
    <b-nav-item>Gallery</b-nav-item>
    <b-nav-item>Blog</b-nav-item>
  </b-nav>
    <b-nav-form>
        <b-form-input v-model="search" size="sm" class="mr-sm-2" type="text" placeholder="Search"/>
        <b-button v-on:click="searchElements" size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
      </b-nav-form>
</div>
    <router-view/>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  data () {
    return {
      search: "",
      results: []
    }
  },
  methods: {
     searchElements () {
       let url = "https://api.mercadolibre.com/sites/MLM/search?q=" + this.search;
       console.log(url);
       axios.get(url)
      .then((res) => {
        console.log(res);
        this.results = res.data.results;
      }).catch((err) => {
          console.log(err, 'err' );
      });
     }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
