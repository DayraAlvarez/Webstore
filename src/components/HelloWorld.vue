<template>
  <div class="hello">
    <h1>Santa's warehouse</h1>
    <p>It's never too soonto buy your Christmas presents!</p>
    <li v-for="result in results">
    <router-link :to="{ name: 'Detail', params: { id: result.id }}">{{result.title}}</router-link>

    </li>
  </div>
</template>

<script>
 import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      results: [],
      search : "juguetes"
    }
  },
  created () {
    this.fetchData()
  },
    watch: {
      '$route': 'fetchData'
    },
  methods : {
    fetchData() {
      axios.get("https://api.mercadolibre.com/sites/MLM/search?q=" + this.search)
      .then((res) => {
        this.results = res.data.results;
      }).catch((err) => {
          console.log(err, 'err' );
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0%;
  padding: 0%;
}

h1, h2 {
  font-weight: normal;
}
</style>
