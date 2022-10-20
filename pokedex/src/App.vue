<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/Pokédex_logo.webp" alt="Logotipo da empresa">
      <hr>
      <input class="input" type="text" name="busca"  placeholder="Buscar pokemon pelo nome" v-model="busca">
      <button id="busca" class="button is-link" @click="buscar">Busca</button>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';
export default {
  
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons:[],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0").then(res => {
      console.log("Pegou a lista de pokemons");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  }
  //  computed: {
  //   resultadoBusca: function(){
  //     if(this.buscas == '' || this.busca == ' '){
  //       return this.pokemons;
  //     }else{
  //       return this.pokemons.filter(pokemon => pokemon.name == this.busca);
  //     }
  //   }
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

#busca {
  margin-top: 10px;
}
</style>
