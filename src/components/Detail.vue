<template>
  <div class="detail">
    <h1>{{ name }}</h1>
    <img :src="image">
    <span>{{price}}</span>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Detail',
  data () {
    return {
      name: 'Name',
      image: 'https://www.petdarling.com/articulos/wp-content/uploads/2014/06/como-quitarle-las-pulgas-a-mi-perro.jpg ',
      price: 'price'
    }
  },
   created () {
    this.getProductDetail();
  },
   watch: {
      '$route': 'getProductDetail'
    },
  methods : {
   getProductDetail () {
     axios.get("https://api.mercadolibre.com/items/" + this.$route.params.id)
     .then((res) => {
       this.name = res.data.title;
       this.image = res.data.pictures[0].url;
       console.log('hola');
       console.log(res.data.result);
       this.price = res.data.price;
     }).catch ((err) => {
       console.log(err);
     })

   }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
