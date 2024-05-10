<!-- <template>
  <div>
    <img :src="pokemonImageUrl" alt="Pokemon Image" />
  </div>
</template>

<script>
import { computed, ref, defineProps } from "vue";

const pokeNUmProp =

let pokeNumber = 1 || ;

export default {
  data() {
    return {
      pokemonImageUrl: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokeNumber}.png`,
    };
  },
};
</script>

<style></style> -->
<script setup>
import { ref, defineProps } from "vue";

const props = defineProps();

const pokemonData = ref({});

const updatePokemonData = (data) => {
  pokemonData.value = data;
  console.log("Updated Pokemon Data:", data); // Add this line to log the received data
};

// Listen for the emitted event
const handlePokemonClicked = (data) => {
  updatePokemonData(data);
};

// Define the pokemonImageUrl here
const pokeNumber = 1; // Set a default value for now
const pokemonImageUrl = `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokeNumber}.png`;
</script>
