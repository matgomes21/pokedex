<template>
  <div id="app">
    <div v-for='(poke,index) in pokemons' :key='index'>
      <Pokemon :id='index+1' :name='poke.name' :url='poke.url' />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  data() {
    return {
      pokemons: []
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(data => {
      console.log("GET pokemon list");
      this.pokemons = data.data.results;
    })
  },
  components: {
    Pokemon
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
  margin-top: 60px;
}
</style>
