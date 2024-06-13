<script>
export default {
  props: {
    apiPokemons: String,
    searchTerm: String,
  },
  data() {
    return {
      pokemonList: [],
    };
  },
  created() {
    this.fetchPokemons();
  },
  methods: {
    async fetchPokemons() {
      try {
        const response = await fetch(this.apiPokemons);
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        this.pokemonList = data;
      } catch (error) {
        console.error("Error fetching Pokemon data:", error);
      }
    },

    emitOpenDetail(pokemon) {
      this.$emit("open-detail", pokemon); // Emit event to App.vue
    },
  },
  computed: {
    filteredPokemonList() {
      if (!this.searchTerm) {
        return this.pokemonList;
      }
      return this.pokemonList.filter((pokemon) => {
        return pokemon.name
          .toLowerCase()
          .includes(this.searchTerm.toLowerCase());
      });
    },
  },
};
</script>
<template>
  <ul v-if="pokemonList.length > 0">
    <li v-for="(pokemon, index) in pokemonList" :key="index">
      {{ pokemon.id }} {{ pokemon.name }}
      <img :src="pokemon.image" alt="{{ pokemon.image }}" />
    </li>
  </ul>

  <p v-else>No Pokemon data found.</p>
</template>

<style scoped>
li {
  display: flex;
  flex-direction: row;
  align-items: center;
}
img {
  width: 40px;
}
</style>
