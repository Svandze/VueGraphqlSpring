<template>
  <div class="navbar">
    <div class="logo logo-left">
      <img src="./assets/pokebola.png" alt="Logo">
    </div>
    <div class="logo logo-right">
      <img src="./assets/logo.png" alt="Otro Logo">
    </div>
  </div>
  <div class="image-container">
    <img src="./assets/grande.jpg" alt="Imagen Grande">
    
  </div>
  <div class="title-image">
  <img src="./assets/titulo.png" alt="Imagen Grande">
  </div>
  <HelloWorld msg="Welcome to Your Vue.js App" />
  
  
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

.navbar {
  background-color: #032b5f;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 66px;
  /* Ajustar el valor de la altura al 120% de la altura actual (55px) */
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  z-index: 999;
  /* Asegura que la barra de navegación se muestre por encima de otros elementos */
}

.logo-left,
.logo-right {
  display: flex;
  align-items: center;
}

.logo img {
  height: 40px;
  margin-left: 5px;
}

.content {
  margin-top: 66px;
  /* Ajustar el valor del margen al nuevo tamaño de la barra */
  padding: 20px;

  background-size: cover;
  background-position: center;
}

.image-container {
  background-size: cover;
  background-position: center;
  height: 100vh; /* Ajusta el contenedor al 100% de la altura visible */
  overflow: hidden;
  position: relative;
  margin-top: 0;
}

.image-container img {
  position: absolute;
  top: 8%;
  /* Desplaza la imagen un 20% hacia arriba */
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
}

.image-container h1 {
  color: white;
  text-align: center;
  font-size: 48px;
  margin-top: 20px;

}

.title-image {
  margin-top: 20px;
  margin-bottom: 90px;
}
</style>
