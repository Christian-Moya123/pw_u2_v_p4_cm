<template>
    <div>
        <h1 v-if="!pokemonCorrecto">Espera por favor......</h1>
        <div v-if="pokemonCorrecto">
            <h1>Juego Pokémon</h1>
            <PokemonImg :pokemonId="pokemonCorrecto.id" :muestraPokemon="showPokemon" />
            <PokemonOps :options="pokemonsArray" v-on:seleccionado="revisarSeleccion($event)" />

            <h1 v-if="showWin" class="win">¡GANASTE! Tu puntaje es: {{ puntos }}</h1>
            <h1 v-if="showLose" class="lose">¡PERDISTE! Intentos agotados.</h1>

            <button v-if="showWin || showLose" @click="reiniciarJuego">Reiniciar Juego</button>
        </div>
    </div>
</template>
  
<script>
import PokemonImg from "../Pokemonimg.vue";
import PokemonOps from "../PokemonOps.vue";
import getPokemonFacade from "../helpers/clientePokemonApi";

export default {
    data() {
        return {
            pokemonsArray: [],
            pokemonCorrecto: null,
            showPokemon: false,
            showWin: false,
            lose: false
        };
    },
    components: {
        PokemonImg,
        PokemonOps,
    },


    methods: {
        async loadStartGame() {
            //llama al metodo interfaz del cliente, que devuelve un arreglo de 4 pokemon
            const arregloPokemons = await getPokemonFacade();
            console.log(arregloPokemons)
            this.pokemonsArray = arregloPokemons
            const indicePokemon = Math.floor(Math.random() * 4)
            this.pokemonCorrecto = this.pokemonsArray[indicePokemon]
        },

        revisarSeleccion(idSeleccionado) {
            console.log('evento en el padre')
            this.showPokemon = true
            console.log(idSeleccionado)

            this.showPokemon =
                idSeleccionado == this.pokemonCorrecto.id ? true : false;
            this.lose = !this.showPokemon;

        }
    },
    mounted() {
        console.log("se monto el componente");
        this.loadStartGame();
    },




};
</script>
  
<style scoped>
h1 {
    text-shadow: 0 0 1px blue;
}
</style>
  