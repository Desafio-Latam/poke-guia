<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h1 class="display-2 mb-3">{{ titulo }}</h1>
        </div>
        <div class="col-12">
          <input
            type="text"
            class="form-control mb-3"
            placeholder="Busca tu Pokemon"
            v-model="pokemon"
          />
        </div>
        <div class="col-12">
          <button class="btn btn-success mb-4 w-50" @click="buscaPokemon">
            Buscar Pokemon
          </button>
        </div>
        <div class="col-12">
          <h3>Nombre del Pokemon</h3>
          <p>{{ nombrePokemon }}</p>
        </div>
        <div class="col-12">
          <!--seteo src con : para dejarla reactiva-->
          <img
            :src="imagenPoke"
            :alt="nombrePokemon"
            width="200"
            height="auto"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      pokemon: "pikachu", //poner al pikachu
      //Colocamos la direccion de la api
      URL_BASE: "https://pokeapi.co/api/v2/pokemon/",
      pokemonData: [],
    };
  },
  created() {
    this.obtenerPokemon();
  },
  computed: {
    titulo() {
      //titulo es una vmodel reactiva y se llama desde el input
      const titulo = "Listado Poke Api";
      return titulo;
    },
    nombrePokemon() {
      return this.pokemonData.name;
    },
    imagenPoke() {
      return this.pokemonData.sprites.other.home; //poner direccion correcta
    },
  },
  methods: {
    async obtenerPokemon() {
      try {
        //aca con los basckytik  conectamos la direccion, y dejamos establecido
        const req = await fetch(`${this.URL_BASE}${this.pokemon}`);
        const data = await req.json();
        this.pokemonData = data;
      } catch (error) {
        console.error(error);
      }
    },
    buscaPokemon() {
      this.obtenerPokemon();
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
