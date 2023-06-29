    <template>
  <div class="container">
    <div class="calculadora">
      <label class="labelCalculadora" for="">Calculadora</label>
      <button v-on:click="agregarNumero('1')">1</button>
      <button v-on:click="agregarNumero('2')">2</button>
      <button v-on:click="agregarNumero('3')">3</button>
      <button v-on:click="setOperacion('+')">+</button>

      <button v-on:click="agregarNumero('4')">4</button>
      <button v-on:click="agregarNumero('5')">5</button>
      <button v-on:click="agregarNumero('6')">6</button>
      <button v-on:click="setOperacion('-')">-</button>

      <button v-on:click="agregarNumero('7')">7</button>
      <button v-on:click="agregarNumero('8')">8</button>
      <button v-on:click="agregarNumero('9')">9</button>
      <button v-on:click="setOperacion('/')">/</button>

      <button class="botonGrande" v-on:click="agregarNumero('0')">0</button>
      <button v-on:click="resolver">=</button>
      <button v-on:click="setOperacion('*')">*</button>

      <button v-on:click="limpiar">Limpiar</button>

      <label for=""
        ><p>{{ resultado }}</p></label
      >
    </div>
  </div>
</template>


<script>
export default {
  name: "Calculadora",
  data() {
    return {
      resultado: "",
      operandoa: 0,
      operandob: 0,
      operacion: "",
    };
  },
  computed: {
    resultadoNumerico() {
      return parseFloat(this.resultado);
    },

    agregarNumero() {
      return (numero) => {
        this.resultado += numero;
      };
    },

    limpiar() {
      return () => {
        this.resultado = "";
      };
    },

    resetear() {
      return () => {
        this.resultado = "";
        this.operandoa = 0;
        this.operandob = 0;
        this.operacion = "";
      };
    },

    resolver() {
      const operandoa = parseFloat(this.resultado.split(this.operacion)[0]);
      const operandob = parseFloat(this.resultado.split(this.operacion)[1]);
      let res = 0;

      if (this.operacion === "+") {
        res = operandoa + operandob;
      } else if (this.operacion === "-") {
        res = operandoa - operandob;
      } else if (this.operacion === "*") {
        res = operandoa * operandob;
      } else if (this.operacion === "/") {
        res = operandoa / operandob;
      }

      this.resultado = res.toString();
    },

    setOperacion() {
      return (op) => {
        if (this.operandoa !== "") {
          this.operacion = op;
          this.resultado += op;
        }
      };
    },
  },
};
</script>
        
        
        
<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.8);
}

.calculadora {
  display: grid;
  grid-template-columns: repeat(4, 100px);
  grid-gap: 10px;
  background-color: #f2f2f2;
  padding: 20px;
  border-radius: 10px;
}

.calculadora button {
  padding: 10px;
  border: none;
  border-radius: 5px;
  background-color: #604caf;
  color: #fff;
  font-size: 18px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.calculadora button:hover {
  background-color: #45a049;
}

.resultado {
  grid-column: span 4;
  margin-top: 10px;
  padding: 10px;
  background-color: #fff;
  border: 2px solid #4caf50;
  border-radius: 5px;
  text-align: right;
  font-size: 24px;
  font-weight: bold;
}

.labelCalculadora {
  grid-column: span 4;
  margin-bottom: 10px;
  padding: 10px;
  background-color: #4caf50;
  color: #fff;
  text-align: center;
  font-size: 20px;
  font-weight: bold;
}
</style>