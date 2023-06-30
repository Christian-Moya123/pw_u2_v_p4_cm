<template>
    <h1>Opciones Pokemon</h1>

    <div class="contenedor-opciones"> 
    <ul>

     

        <li v-for="pokemon in opciones" :key="pokemon.id">{{ pokemon.nombre }}</li>

    </ul>
    </div>
</template>
  
<script>
export default {   
    
    props:{
                Opciones:{
                    type: Array,
                    required: true
                }
    }

}
</script>
  
<style scoped>

ul{
    list-style-type:none ;
}

li{
    border: 1px solid rgba(233,0,0,0.2);
    border-radius:5px ;
    background: white;
    margin-bottom: 10px;
    width: 200px;
    cursor: pointer;
}

li:hover{
    background: aquamarine;
}

.contenedor-opciones{
    display: flex;
    justify-content: center;
}

</style>