<script>
import axios from 'axios';
import PokemonCard from './components/PokemonCard.vue';

export default { 
  name: 'App', 
  data() { 
    return { 
      pokemons: [], // Arreglo de pokémons a mostrar 
      discoveredCount: 0 // Contador de pokémons descubiertos 
    }; 
  }, 
  components: { 
    PokemonCard 
  }, 
  methods: { // Método para incrementar el contador de pokémons descubiertos 
    incrementDiscovered() { 
      this.discoveredCount++; 
    } 
  }, 
  async created() { // Consumir la API de PokéAPI para obtener datos de los pokémons 
    const promises = []; 
    for (let i = 1; i <= 20; i++) { 
      promises.push(axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)); 
    } 
    const responses = await Promise.all(promises); 
    this.pokemons = responses.map(response => ({ 
      name: response.data.name, 
      image: response.data.sprites.front_default 
    })); 
  } 
};
</script>

<template>
  <div id="app"> <!-- Logo de Pokémon --> <img src="./assets/img/pokemon.png" alt="Pokémon Logo" class="logo" />
    <!-- Título y contador de pokémons descubiertos -->
    <h1>¿Quién es ese Pokémon?</h1>
    <p>Pokémons descubiertos: {{ discoveredCount }}</p> <!-- Contenedor de las tarjetas de pokémon -->
    <div class="pokemon-container">
      <PokemonCard v-for="(pokemon, index) in pokemons" :key="index" :pokemon="pokemon"
        @discovered="incrementDiscovered" />
    </div>
  </div>
</template>

<style scoped>
/* Estilos básicos para el componente principal */
#app {
  text-align: center;
  margin-top: 20px;
}

.logo {
  width: 250px;
  height: 100px;
  margin-bottom: 20px;
}

.pokemon-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  justify-items: center;
}
</style>
