<template>
  <div>
    <a target="_blank">
      <img src="./assets/pokemonLogo.svg" class="logo" alt="PokeLogo" />
    </a>
  </div>
  <p>Find Pokemon: {{ filterText }}</p>
  <input type="text" v-model="filterText" />
  <div>
    <ul>
      <PokedexCard
        v-for="(pokemon, index) in storedPokemon.filteredListOfPokemon"
        :key="`poke-${index}`"
        :number="pokemon.entry_number"
        :name="pokemon.pokemon_species.name"
      />
      <!-- #{{ pokemon.entry_number }} - {{ pokemon.pokemon_species.name }} -
        {{ pokemon.pokemon_species.url }} -->
      <!-- </PokedexCard> -->
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted, computed, reactive } from "vue";
import PokedexCard from "./components/PokedexCard.vue";

const pokemonList = ref([]);
const filterText = ref("");

const storedPokemon = reactive({
  list: [],
  filteredListOfPokemon: computed(() =>
    storedPokemon.list.filter((pokemon) =>
      pokemon.pokemon_species.name.includes(filterText.value)
    )
  ),
});

onMounted(async () => {
  const pokeData = await fetch("https://pokeapi.co/api/v2/pokedex/2/").then(
    (response) => response.json()
  );

  storedPokemon.list = pokeData.pokemon_entries;
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
