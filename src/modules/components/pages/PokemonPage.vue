<template>
    <h1>Juego Pokemon</h1>
    <Pokemonimg :pokemonId= "59" :muestraPokemon="true"/>
    <PokemonOps />
</template>

<script>
import Pokemonimg from '../Pokemonimg.vue'
import PokemonOps from '../PokemonOps.vue'

export default {
    components: {
        Pokemonimg,
        PokemonOps,
    }

}
</script>

<style></style>