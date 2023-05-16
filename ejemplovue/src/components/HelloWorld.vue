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
    

    <div v-if="pokemon1 && pokemon2">
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

    <div v-if="ganador">
      <h3>Ganador de la batalla:</h3>
      <p>Nombre: {{ ganador.nombre }}</p>
      <p>Nombre: {{ ganador.tipo }}</p>
      <p>Nombre: {{ ganador.nivel }}</p>

    </div>

  </div>
  <button @click="iniciarBatalla">Iniciar Batalla Pokémon</button>
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
        this.pokemon1 = batalla.pokemon1;
        this.pokemon2 = batalla.pokemon2;
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
<style>
  .pokemon-box {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
  }
</style>
