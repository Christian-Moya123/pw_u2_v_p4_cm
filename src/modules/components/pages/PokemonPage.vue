<template>
    <div>
        <h1 v-if="!pokemonCorrecto">Espera por favor......</h1>
        <div v-if="pokemonCorrecto">
            <h1>Juego Pokémon</h1>
            <Pokemonimg :pokemonId="pokemonCorrecto.id" :muestraPokemon="showPokemon" />
            <PokemonOps :options="pokemonsArray" v-on:seleccionado="revisarSeleccion($event)" />

            <h1 v-if="showWin" class="win">¡GANASTE! Tu puntaje es: {{ puntos }}</h1>
            <h1 v-if="showLose" class="lose">¡PERDISTE! Intentos agotados.</h1>

            <button v-if="showWin || showLose" @click="reiniciarJuego">Reiniciar Juego</button>
        </div>
    </div>
</template>
  
<script>
import Pokemonimg from "../Pokemonimg.vue";
import PokemonOps from "../PokemonOps.vue";
import getPokemonFacade from "../helpers/clientePokemonApi";


export default {
    data() {
        return {
            pokemonsArray: [],
            pokemonCorrecto: null,
            showPokemon: false,
            showWin: false,
            showLose: false,
            puntos: 0,
            intentos: 0,
        };
    },
    components: {
        Pokemonimg,
        PokemonOps,
    },

    methods: {
        async loadStartGame() {
            const arregloPokemons = await getPokemonFacade();
            this.pokemonsArray = arregloPokemons;
            const indicePokemon = Math.floor(Math.random() * 4);
            this.pokemonCorrecto = this.pokemonsArray[indicePokemon];
        },

        revisarSeleccion(idSeleccionado) {
            this.showPokemon = true;
            this.intentos++;

            if (idSeleccionado === this.pokemonCorrecto.id) {
                this.showWin = true;
                this.puntos = this.calcularPuntos();
            } else {
                if (this.intentos >= 3) {
                    this.showLose = true;
                }
            }
        },

        calcularPuntos() {
            if (this.intentos === 1) {
                return 5;
            } else if (this.intentos === 2) {
                return 2;
            } else if (this.intentos === 3) {
                return 1;
            }
        },

        reiniciarJuego() {
            this.pokemonCorrecto = null;
            this.showPokemon = false;
            this.showWin = false;
            this.showLose = false;
            this.puntos = 0;
            this.intentos = 0;
            this.loadStartGame();
        },
    },

    mounted() {
        this.loadStartGame();
    },
};
</script>

<style scoped>
h1 {
    text-shadow: 0 0 1px blue;
}


.lose {
    margin-top: 20px;
}

button {
    margin-top: 20px;
}
</style>