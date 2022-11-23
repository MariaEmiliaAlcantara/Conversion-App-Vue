<template>
  <main class="wrapper">
    <h3>Conversão Imediata</h3>
    <p>Cotação do dólar atualizada: R${{ conversion.ask }}</p>

    <label>
      <input
        type="number"
        placeholder="Quantidade em reais"
        v-model="totalReais"
        v-on:input="handleInputChange"
      />
    </label>

    <div class="container-buttons">
      <button v-on:click="handleCleanInput">Limpar</button>
      <button v-on:click="handleCalculate">Calcular</button>
    </div>

    <p v-if="showParagraph">
      Com R${{ totalReais.toFixed(2).replace(".", ",") }} é possível comprar
      USD{{ totalDolars.toFixed(2).replace(".", ",") }}
    </p>
  </main>
</template>

<script>
import axios from "axios";

export default {
  name: "Conversion-Vue",
  data() {
    return {
      totalReais: "",
      totalDolars: 0,
      conversion: {},
      showParagraph: false,
      message: "",
    };
  },
  methods: {
    async getConversion() {
      try {
        const response = await axios.get(
          "https://economia.awesomeapi.com.br/last/USD-BRL"
        );
        this.conversion = response.data.USDBRL;
      } catch (err) {
        console.log(err);
      }
    },
    handleCleanInput() {
      this.showParagraph = false;
      this.totalReais = "";
    },
    handleCalculate() {
      this.showParagraph = true;
      this.totalDolars = this.totalReais / this.conversion.ask;
    },
    handleInputChange() {
      this.showParagraph = false;
    },
  },
  beforeMount() {
    this.getConversion();
  },
  watch: {},
};
</script>

<style scoped>
.wrapper {
  height: 90vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start;
  margin-top: 4rem;
  gap: 2rem;
  padding: 2rem 0;
  color: #4a3337;
}

.wrapper h3 {
  font-size: 2rem;
}

.wrapper input {
  background-color: transparent;
  color: #4a3337;
  border: 2px solid #4a3337;
  border-radius: 8px;
  padding: 0 1rem;
  height: 3rem;
  width: 20rem;
  font-size: 0.875rem;
  outline: none;
}

.container-buttons {
  display: flex;
  gap: 0.5rem;
}
.container-buttons button {
  background-color: #4a3337;
  color: white;
  border: none;
  border-radius: 8px;
  height: 2rem;
  width: 8rem;
  cursor: pointer;
  transition: all 0.2s;
}

.container-buttons button:hover {
  opacity: 0.8;
}
</style>
