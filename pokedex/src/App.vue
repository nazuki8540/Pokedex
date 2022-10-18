<template>
  <div id="app">
    <div v-for="(poke,index) in pokemons" :key="index">
      <h1>{{ index + 1 }} {{poke.name}}</h1>
    </div>
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
      this.pokemons = res.data.results;
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
