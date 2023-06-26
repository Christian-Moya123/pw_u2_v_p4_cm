<template>
  
  
  <Juego1 />
</template>


<script>
import CaracolaMagica from './components/CaracolaMagica.vue';
import Juego1 from './components/Juego1.vue';
import PokemonPage from './modules/components/pages/PokemonPage.vue';
import Calculadora from './components/Calculadora.vue';



export default {
  name: 'App',
  components: {
    //Calculadora
    //CaracolaMagica
    Juego1
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
