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

<br>
  <button @click="iniciarBatalla" class="btn-pokemon">Iniciar Batalla Pokémon</button>
  <br>  
  <div  class="pokemon-box-2"  v-if="pokemon1 && pokemon2">
      <h3>Pokémones en batalla:</h3>
      <h3>Pokemon 1:</h3>
      <p>Nombre: {{ pokemon1.nombre }}</p>
      <p>Tipo: {{ pokemon1.tipo }}</p>
      <p>Nivel: {{ pokemon1.nivel }}</p>
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
  color: #42b983;
}

.btn-pokemon {
  background-color: transparent;
  color: #4CAF50;
  padding: 10px 20px;
  border: 2px solid #4CAF50;
  border-radius: 4px;
  cursor: pointer;
}

.btn-pokemon:hover {
  background-color: #4CAF50;
  color: white;
}
</style>
<style>
  .pokemon-box {
    border: 1px solid #4CAF50;
  padding: 10px;
  margin-bottom: 10px;
  background-color: #f2f2f2; /* Color de fondo */
  color: #333; /* Color del texto */
  }
  .pokemon-box-2 {
    border: 1px solid #4CAF50;
  padding: 20px; /* Ajusta el tamaño del padding según tus preferencias */
  margin: 10px; /* Ajusta el tamaño del margen según tus preferencias */
  background-color: #d7f2d9; /* Cambia el color de fondo a un verde más claro */
  color: #333; /* Color del texto */
  }
</style>
