<template>
    <h1>Juego Pokemon</h1>
    <Pokemonimg :pokemonId= "59" :muestraPokemon="true"/>

    <PokemonOps :opciones="pokemonArray" />
</template>

<script>
import Pokemonimg from '../Pokemonimg.vue'
import PokemonOps from '../PokemonOps.vue'
import obtenerFachadaPokemons from "../helpers/clientePokemonApi"

//console.log(obtenerFachadaPokemons())

export default {
    components: {
        Pokemonimg,
        PokemonOps,

    },


    methods:{
    async cargaJuegoInicial(){
        const arregloPokemons = await obtenerFachadaPokemons()
        console.log(arregloPokemons)

    }

    },

    mounted(){
        console.log("se monto el  componente")
        this.cargaJuegoInicial()
    }

}
</script>

<style></style>