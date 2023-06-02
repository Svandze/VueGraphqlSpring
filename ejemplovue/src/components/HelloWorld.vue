<template>
  <div>
    <li v-for="pokemon in pokemons" :key="pokemon.pokemonId">
  <div class="pokemon-box">
    <div>
      <p>Nombre:{{ pokemon.nombre }}</p>
    </div>
    <div>
      <p>nivel: {{ pokemon.nivel }}</p>
    </div>
    <div>
      <p>tipo: {{ pokemon.tipo }}</p>
    </div>
  </div>
</li>
<div class="title-image">
  <img src="./battle.png" >
  </div>
<br>
  <button @click="iniciarBatalla" class="btn-pokemon">Iniciar Batalla Pokémon</button>
  <br>  
  <div  class="pokemon-box-2"  v-if="pokemon1 && pokemon2">
      <h3>Pokémones en batalla:</h3>
      <h3>Pokemon 1:</h3>
      <p>Nombre: {{ pokemon1.nombre }}</p>
      <p>Tipo: {{ pokemon1.tipo }}</p>
      <p>Nivel: {{ pokemon1.nivel }}</p>

      
    </div>
    <div  class="pokemon-box-2"  v-if="pokemon1 && pokemon2">
      <h3>Pokémones en batalla:</h3>
      <h3>Pokemon 2:</h3>
      <p>Nombre: {{ pokemon2.nombre }}</p>
      <p>Tipo: {{ pokemon2.tipo }}</p>
      <p>Nivel: {{ pokemon2.nivel }}</p>
    </div>
    <div class="pokemon-box-2" v-if="ganador">
      <h3>Ganador de la batalla:</h3>
      <p>Nombre: {{ ganador.nombre }}</p>
      <p>tipo: {{ ganador.tipo }}</p>
      <p>Nivel: {{ ganador.nivel }}</p>

    </div>

  </div>
  
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      pokemons: [],
      ganador: null,
      pokemon1: null,
      pokemon2: null
    };
  },
  methods: {
    async iniciarBatalla() {
      try {
        const response = await axios.post("https://batallas-dot-crack-photon-385921.ue.r.appspot.com/apis/graphql", {
          query: `
          mutation {
  batallaPokemon {
    batallaId
    ganador {
      nombre
      tipo
      nivel
    }
    pokemon1 {
      nombre
      tipo
      nivel
    }
    pokemon2 {
      nombre
      tipo
      nivel
    }
  }
}
          `
        });

        const batalla = response.data.data.batallaPokemon;
        console.log(batalla);
        this.ganador = batalla.ganador;
        this.pokemon1 = batalla.pokemon1;
        this.pokemon2 = batalla.pokemon2;
      } catch (error) {
        console.error(error);
      }
    },
    async batallaPokemon() {
      try {
        const response = await axios.post("https://consultas-dot-crack-photon-385921.ue.r.appspot.com/apis/graphql", {
          query: `
            query {
              findAllPokemons {
                nombre
                tipo
                nivel
              }
            }
          `
        });

        this.pokemons = response.data.data.findAllPokemons;
        console.log(this.pokemons);
      } catch (error) {
        console.error(error);
      }
    }
  },
  async mounted() {
    await this.batallaPokemon();
  }
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #032b5f;
}

.btn-pokemon {
  background-color: transparent;
  color: #032b5f;
  padding: 10px 20px;
  border: 2px solid #032b5f;
  border-radius: 4px;
  cursor: pointer;
}

.btn-pokemon:hover {
  background-color: #d3f307;
  color: rgb(1, 1, 1);
}


</style>
<style>
  .pokemon-box {
    width: 280px;
      background-color: #032b5f;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      padding: 20px;
      margin: 20px;
      display: inline-block;
      vertical-align: top;
      color: #f9f8f8; /* Color del texto */
  }
  .pokemon-box-2 {
    width: 280px;
      background-color: #032b5f;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      padding: 20px;
      margin: 20px;
      display: inline-block;
      vertical-align: top;
      color: #f9f8f8; /* Color del texto */
  }
</style>
