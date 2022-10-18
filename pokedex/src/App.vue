<template>
  <div id="app">

  </div>
</template>
<script>
import axios from 'axios';
export default {
  name: 'App',
  data(){
    return{
      pokemons: []
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0").then(res => {
      console.log("Pegou a lista de pokemons");
      this.pokemns = res.data.results;
    }).catch(err => {
      console.log(err);
    })
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}



</style>
