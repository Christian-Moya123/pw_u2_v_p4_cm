<template>
    <h1>Ejemplo de consumo API</h1>
    <img v-if="urlImagen" :src="urlImagen" alt="No se puede presentar">
    <input v-model=pregunta type="text" placeholder="Hazme una pregunta">
    <div class="bg-dark"></div>
    <div class="container">
        <input v-model=pregunta type="text" placeholder="Hazme una pregunta">

        <div>
            <p>Recuerda terminar con un enter la pregunta</p>
            <p>Si consigues 3 sí seguidos, GANAS</p>
        </div>

        <div>
            <h2>{{ pregunta }}</h2>
            <h1>{{ respuesta }}</h1>
            <h1># de si: {{ contadorSi }}</h1>
            <h1># de no: {{ contadorNo }}</h1>
            <h1 v-if="gano">3 "SI" conseguidos GANASTE </h1>
            <h1 v-if="perdio">3 "NO" conseguidos PERDISTE </h1>
        </div>

    </div>
    <Button v-on:click="resetear">Resetear</Button>
</template>
  
<script>
export default {

    data() {
        return {
            pregunta: '',
            respuesta: '',
            urlImagen: null,
            contadorSi: 0,
            contadorNo: 0,
            gano: false,
            perdio: false
        }
    },

    watch: {
        pregunta(value, oldValue) {
            console.log(value);
            console.log(oldValue);
            //Valida si el valor nuevo incluye el signo de ?
            if (value.includes('?')) {
                console.log('Consumir el API');
                this.respuesta = "Espere favor....."
                this.consumirAPI()
            }
        }
    },

    methods: {
        async consumirAPI() {
            const { answer, image } = await fetch('https://yesno.wtf/api').then(r => r.json());

            this.respuesta = answer;
            this.urlImagen = image;
            console.log(this.respuesta)
            console.log(this.urlImagen)

            this.respuestaContador()
            this.validarRespuesta()
        },
        validarRespuesta() {
            if (this.contadorSi === 3) {
                this.gano = true
            } if (this.contadorNo === 3) {
                this.perdio = true
            }



        },

        respuestaContador() {
            if (this.respuesta === 'yes') {
                this.contadorSi += 1;
            } else {
                this.contadorNo += 1;
            }
        },
        resetear() {
            this.pregunta = '';
            this.respuesta = '';
            this.urlImagen = null;
            this.contadorSi = 0;
            this.contadorNo = 0;
            this.gano = false;
            this.perdio = false;
        }




    },



}
</script>
  
<style>
img,
.bg-dark {
    height: 100vh;
    width: 100vw;
    left: 0px;
    max-width: 100%;
    max-height: 100%;
    position: fixed;
    top: 0px;
}

.bg-dark {
    background-color: rgba(0, 0, 0, 0.3);
}

.container, button{
    position: relative;
}



input {
    width: 250px;
    padding: 10px 15px;
    border-radius: 5px;
    border: none;
}

p,
h1,
h2 {
    color: white;
}

p {
    font-size: 20px;
    margin-top: 10px;
}
</style>

