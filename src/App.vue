<template>
  <HeaderVue></HeaderVue>
  <ConversionVue />
</template>

<script>
import HeaderVue from "./components/Header.vue";
import ConversionVue from "./components/Conversion.vue";

export default {
  name: "App",
  components: {
    HeaderVue,
    ConversionVue,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
}
a {
  text-decoration: none;
  color: var(--black);
}

body {
  width: 100vw;
  height: 100vh;
  background-color: #d3cdbf;
}
</style>
