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
  <p>Find Pokemon: {{ filterText }}</p>
  <input type="text" v-model="filterText" />
  <div>
    <ul>
      <li
        v-for="(pokemon, index) in filteredPokemonList"
        :key="`poke-${index}`"
      >
        #{{ pokemon.entry_number }} - {{ pokemon.pokemon_species.name }} -
        {{ pokemon.pokemon_species.url }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";

const pokemonList = ref([]);
const filterText = ref("");
const filteredPokemonList = computed(() => {
  return pokemonList.value.filter((pokemon) => {
    return pokemon.pokemon_species.name.includes(filterText.value);
  });
});

onMounted(async () => {
  const pokeData = await fetch("https://pokeapi.co/api/v2/pokedex/2/")
    .then((response) => response.json())
    .then((data) => {
      pokemonList.value = data.pokemon_entries;
    });
});
</script>

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
