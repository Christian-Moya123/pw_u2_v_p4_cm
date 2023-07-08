<template>
	<div class="container">
		<h1 v-if="!pokemonCorrecto">Espera por favor......</h1>
		
		<div v-else>
			
			<h1>Juego pokemon</h1>
			
			<PokemonImg class="imagen" :pokemonId="pokemonCorrecto.id" :muestraPokemon="showPokemon" />
			<PokemonOps v-show="!showResult" :options="pokemonsArray" v-on:seleccionado="revisarSeleccion($event)" />
			<h3 v-if="showLose && !showResult">Prueba otro!</h3>
		</div>

		<div v-if="showResult">
			<div v-if="showWin">
				<h1>Ganaste</h1>
				<div class="result">
					<p><b>Puntaje:</b> {{ this.puntaje }}</p>
					<p><b>Intentos:</b> {{ this.intentos }}</p>
				</div>
			</div>
			<h1 v-else>Perdiste</h1>
			<button @click="reiniciar()">REINICIAR</button>
		</div>
	</div>
</template>

<script>

import PokemonImg from "../components/PokemonImg.vue";
import PokemonOps from "../components/PokemonOps.vue";

//Se importa el metodo fachada del cliente
import getPokemonFacade from '../helpers/clientePokemonAPI'
export default {

	data() {
		return {
			pokemonsArray: [],
			pokemonCorrecto: null,
			showPokemon: false,
			showWin: false,
			showResult: false,
			puntaje: 0,
			intentos: 0,
			showLose: false,
		}
	},
	components: {
		PokemonImg,
		PokemonOps,
	},
	methods: {
		//metodo que se ejecuta siempre cuando el componente se monta al DOM(es especial)

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
			this.intentos += 1
			console.log(idSeleccionado)

			if (idSeleccionado === this.pokemonCorrecto.id) {
				this.showWin = true
				this.showResult = true
				this.acumulacionPuntos()
			} else {
				this.showLose = true
			}
			this.conteoIntentos()
			this.showPokemon = true

		},

		acumulacionPuntos() {

			if (this.intentos === 1) {
				console.log("ganaste")
				this.puntaje= 5;

			} else if (this.intentos === 2) {
				this.puntaje=  2;
			} else if (this.intentos === 3) {
				this.puntaje=  1;
			}

		},

		conteoIntentos() {
			if (this.intentos == 3 && !this.showWin) {
				this.showResult = true
			}
		},

		reiniciar() {
			this.pokemonsArray = []
			this.pokemonCorrecto = null
			this.showPokemon = false
			this.showWin = false
			this.showResult = false
			this.puntaje = 0
			this.intentos = 0
			this.loadStartGame()
			this.showLose = false
		},
	},
	mounted() {
		console.log("se monto el componente");
		this.loadStartGame();
	},

}
</script>

<style>
.result {
	display: flex;
	flex-direction: row;
	align-content: center;
	justify-content: center;
	gap: 100px;
}

.whos {
	height: 100px;
}


</style>