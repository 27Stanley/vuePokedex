<script setup>
import { onMounted, ref } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import Button from "@mui/material/Button";
</script>

<script>
export default {
  data: () => ({
    pokemonList: [],
  }),
  async mounted() {
    const pokeData = await fetch("https://pokeapi.co/api/v2/pokedex/2/").then(
      (response) => response.json()
    );

    this.pokemonList = pokeData.pokemon_entries;
  },
};
</script>
<!-- <script>
const pokemonList = ref([]);

async function kantoPokemon() {
  const response = await fetch("https://pokeapi.co/api/v2/pokedex/2/");
  const pokeData = await response.json();
  const pokemon = pokeData.pokemon_entries;

  pokemonList = pokemon.map((pokemon) => ({
    entryNumber: pokemon.entry_number,
    pokeName: pokemon.pokemon_species.name,
    url: pokemon.pokemon_species.url,
  }));
}
</script> -->

<template>
  <div>
    <a target="_blank">
      <img src="./assets/pokemonLogo.svg" class="logo" alt="PokeLogo" />
    </a>
  </div>
  <HelloWorld msg="Pokedex" />
  <div>
    <button @click="logKantoPokemon">consoleLogKantoPokemon</button>
  </div>

  <div>
    <ul>
      <li v-for="(pokemon, index) in pokemonList" :key="`poke-${index}`">
        {{ pokemon.entry_number }}
        {{ pokemon.pokemon_species.name }}
        {{ pokemon.pokemon_species.url }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
