<template>
  <div class="hello">
    <h1>Items</h1>
    <li v-for="result in results">
      <router-link to="/detail/{{result.id}}">{{ result.title }}</router-link>{{ result.title }}
    </li>
  </div>
</template>

<script>
 import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      results: []
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
      alert('sas');
      axios.get("https://api.mercadolibre.com/sites/MLA/search?q=juguetes")
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
h1, h2 {
  font-weight: normal;
}
</style>
