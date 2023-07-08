<template>
  <h1>Bienvenido al juego</h1>

  <img src="https://i.pinimg.com/originals/fd/18/c6/fd18c6d26d4d9d26a0bd9d1a2fb2bd04.png" alt="No cargola imagen">

  <div class="container">
    <p><b>Reglas</b></p>
    <h3>
      Debes adivinar el nombre del pokemon oculto, si lo haces ganaras un premio

      Solo tienes 3 intentos para poder adivinar el pokemon correcto
    </h3>
    <h3>Asignacion de puntos</h3>
    <p>El puntaje dependera de en cuantos intentos logras adivinar cual es la opcion correcta</p>
    <h3>
      Un intento: 5 puntos<br />
      Dos intento: 2 puntos<br />
      Tres intento: 1 punto
    </h3>

    <h3><b>Mientras mas puntos obtengas mejor será tu premio</b></h3>

  </div>
</template>

<script>
export default {

}
</script>

<style>
h1 {
  color: rgb(73, 0, 0);
}

.container{
  background: rgb(255, 0, 0);
  font-size: 40px;
  color: white;
}

img{
  height:500px
}
</style>