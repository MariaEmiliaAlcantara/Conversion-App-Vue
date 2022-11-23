<template>
  <main class="wrapper">
    <h3>Conversão Imediata</h3>
    <p>Cotação do dólar atualizada: {{ conversion.ask }}</p>
    <p>Insira abaixo a quantidade em reais</p>
  </main>
</template>

<script>
import axios from "axios";

export default {
  name: "Conversion-Vue",
  data() {
    return {
      conversion: {},
    };
  },
  methods: {
    async getConversion() {
      const response = await axios.get(
        "https://economia.awesomeapi.com.br/last/USD-BRL"
      );
      this.conversion = response.data.USDBRL;
    },
  },
  beforeMount() {
    this.getConversion();
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  padding: 2rem 0;
  color: #4a3337;
}

.wrapper h3 {
  font-size: 2rem;
}
</style>
