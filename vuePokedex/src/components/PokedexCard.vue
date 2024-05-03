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
    console.log(
      currentPokemonEntry.stats,
      currentPokemonEntry.types,
      currentPokemonEntry.sprites.front_default
    );
  } catch (err) {
    console.log("error", err);
  }
};
</script>

<template>
  <li class="pokeListItem">
    Pokedex entry no. #{{ number }}:
    <button class="pokeButton" @click="handleClick">{{ displayName }}</button>
  </li>
</template>

<style>
.pokeListItem {
  display: flex;
  align-items: center;
  padding: 10px;
}

.pokeButton {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition:
    border-color 0.25s,
    filter 0.25s;
  margin-left: 20px;
  width: 100%;
}

@media (min-width: 768px) {
  .pokeButton {
    width: 150px;
  }
}

.pokeButton:hover {
  filter: drop-shadow(0 0 2em #fdd54faa);
}

.pokeButton:focus,
.pokeButton:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}
</style>
