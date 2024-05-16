<script setup>
import { ref, onMounted, computed, reactive } from "vue";

const pokeGenerations = {
  Kanto: 2,
  Johto: 3,
  Hoenn: 4,
  Sinnoh: 5,
  Unova: 6,
  Kalos: 7,
  Alola: 8,
  Galar: 9,
  Pandea: 10,
};
</script>

<template>
  <div class="pokedexGenerations">
    <div v-for="(generation, key) in pokeGenerations" :key="key">
      <button @click="selectGeneration(key)">{{ key }}</button>
    </div>
  </div>
</template>

<style scoped>
.pokedexGenerations {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: stretch;
  justify-content: center;
  width: 100%;
}

.pokedexGenerations button {
  width: 70px;
  padding: 5%;
  margin: 5px;
  margin-left: 15px;
  margin-right: 15px;
}
</style>
