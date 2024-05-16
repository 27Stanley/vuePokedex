<template>
  <div class="container">
    <div class="logoContainer">
      <a target="_blank">
        <img src="./assets/pokemonLogo.svg" class="logo" alt="PokeLogo" />
      </a>
    </div>

    <div class="PokedexRegion">
      <PokedexRegion />
    </div>

    <div class="sideBar">
      <div class="searchPokemon">
        <h2>Find Pokemon: {{ filterText }}</h2>
        <input type="text" v-model="filterText" style="width: 100%" />
      </div>

      <div class="pokedexList">
        <ul style="list-style-type: none">
          <PokedexCard
            v-for="(pokemon, index) in storedPokemon.filteredListOfPokemon"
            :key="`poke-${index}`"
            :number="pokemon.entry_number"
            :name="pokemon.pokemon_species.name"
          />
        </ul>
      </div>
    </div>

    <div class="displaySelectedPokemon">
      <p>Poke Main Display</p>
      <PokemonCardMain />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed, reactive } from "vue";
import PokedexCard from "./components/PokedexCard.vue";
import PokedexRegion from "./components/PokedexRegion.vue";
import PokemonCardMain from "./components/PokemonCardMain.vue";

// const pokemonList = ref([]);
const filterText = ref("");
const pokedexRegion = 2;

const storedPokemon = reactive({
  list: [],
  filteredListOfPokemon: computed(() =>
    storedPokemon.list.filter((pokemon) =>
      pokemon.pokemon_species.name.includes(filterText.value)
    )
  ),
});

onMounted(async () => {
  const pokeData = await fetch(
    `https://pokeapi.co/api/v2/pokedex/${pokedexRegion}/`
  ).then((response) => response.json());

  storedPokemon.list = pokeData.pokemon_entries;

  // const fetchThePokedex = await fetch("/.netlify/functions/fetchPokedex").then(
  //   (response) => {
  //     console.log("here", response);
  //     console.log(response.json());
  //   }
  // );

  // storedPokemon.list = fetchPokedex.pokemon_entries;
});
</script>

<style>
.logo {
  height: 6em;
  padding: 1.5em;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.container {
  display: grid;
  grid-template-columns: 1fr 3.2fr 0.6fr;
  gap: 10px;
  width: 90%;
}

.logoContainer {
  grid-column-start: 2;
  grid-column-end: 3;
  grid-row: 1;
}

.sideBar {
  grid-column-start: 1;
  grid-column-end: 2;
  background-color: #464646;
  border-radius: 10px;
  padding: 20px;
  height: 100vh;
  margin: 0;
}

.searchPokemon {
  padding-bottom: 20px;
  /* display: flex;
  justify-content: flex; */
}

.displaySelectedPokemon {
  grid-column-start: 2;
  grid-column-end: 4;
}

.pokedexList ul {
  margin: 0;
  padding: 10px;
  height: 84vh;
}

.pokedexList {
  overflow-y: auto;
  border: 1px solid#b3b3b3;
  border-radius: 5px;
}

.PokedexRegion {
  grid-column-start: 1;
  grid-column-end: 2;
  grid-row: 1;
}
</style>
