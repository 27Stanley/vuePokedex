<template>
  <div>
    <img :src="pokemonImageUrl" alt="Pokemon Image" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemonImageUrl:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png",
    };
  },
};
</script>
