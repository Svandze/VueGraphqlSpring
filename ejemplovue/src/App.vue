<template>
  <img alt="Vue logo" src="./assets/Imagen1.png" class="logo">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
.logo {
  width: 300px; /* Ancho de la imagen */
  height: auto; /* Altura se ajustará automáticamente manteniendo la proporción */
}
</style>
