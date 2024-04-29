<script setup>
import { computed, ref, defineProps } from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  number: {
    type: Number,
    required: true,
  },
});

const displayName = computed(() => {
  return props.name[0].toUpperCase() + props.name.substring(1);
});

const handleClick = async () => {
  try {
    const pokeLookup = `https://pokeapi.co/api/v2/pokemon/${props.name}`;
    const response = await fetch(pokeLookup);
    const currentPokemonEntry = await response.json();
    console.log(currentPokemonEntry);
  } catch (err) {
    console.log("error", err);
  }
};
</script>

<template>
  <li>Pokedex entry no. #{{ number }}:</li>
  <button @click="handleClick">{{ displayName }}</button>
</template>

<style></style>
