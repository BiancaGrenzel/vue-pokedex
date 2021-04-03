<template>
  <div id="app">
    <div class="container-total">
      <div class="column is-half is-offset-one-quarter container-total">
        <input
          type="text"
          name=""
          id=""
          placeholder="Buscar pokemon"
          v-model="busca"
          class="input is-rounded input-buscar"
        />
        <button class="button is-primary buscar" id="buscaBtn">Buscar</button>

        <div class="scroll-pokemons">
          <div v-for="(poke, index) in resultadoBusca" :key="index">
            <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("Pegou a lista de pokemons.");
        this.pokemons = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  computed: {
    resultadoBusca: function () {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    },
  },
};
</script>

<style>
.container-total {
  padding-top: 0% !important;
}
.scroll-pokemons {
  margin-top: 5%;
  padding-left: 5%;
  padding-right: 5%;
  overflow: auto;
  width: 100%;
  height: 320px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#buscaBtn {
  margin-top: 2%;
}

.input-buscar {
  width: 300px !important;
  margin-right: 5%;
}

.buscar {
  width: 100px;
  margin-top: 0px !important;
}

.column{
  width: 800px !important;
}
</style>
