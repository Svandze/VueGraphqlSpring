<template>
  <div>
    <li v-for="pokemon in pokemons" :key="pokemon.pokemonId">
      {{ pokemon.nombre }} - {{ pokemon.nivel }} - {{ pokemon.tipo }}
    </li>
    <button @click="iniciarBatalla">Iniciar Batalla Pokémon</button>

    <div v-if="ganador">
      <h3>Ganador de la batalla:</h3>
      <p>Nombre: {{ ganador.nombre }}</p>
      <p>Nombre: {{ ganador.tipo }}</p>
      <p>Nombre: {{ ganador.nivel }}</p>

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
      ganador: null
    };
  },
  methods: {
    async iniciarBatalla() {
      try {
        const response = await axios.post("http://localhost:8088/apis/graphql", {
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
      } catch (error) {
        console.error(error);
      }
    },
    async batallaPokemon() {
      try {
        const response = await axios.post("http://localhost:8087/apis/graphql", {
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
</style>
