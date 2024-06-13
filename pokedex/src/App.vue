<script setup>
import SearchBar from "./components/SearchBar.vue";
import PokemonDetail from "./components/PokemonDetail.vue";
import PokemonList from "./components/PokemonList.vue";
</script>

<script>
export default {
  components: {
    SearchBar,
    PokemonList,
    PokemonDetail,
  },
  data() {
    return {
      apiPokemons: "https://pokebuildapi.fr/api/v1/pokemon/limit/100",
      searchTerm: "",
      selectedPokemon: null,
    };
  },
  methods: {
    handleSearch(searchTerm) {
      this.searchTerm = searchTerm;
    },
    openDetail(pokemon) {
      this.selectedPokemon = pokemon;
    },
  },
};
</script>

<template>
  <h1>Pokemons</h1>
  <SearchBar v-model="searchTerm" />
  <PokemonList
    :apiPokemons="apiPokemons"
    :searchTerm="searchTerm"
    @open-detail="openDetail"
  />
  <PokemonDetail v-if="selectedPokemon" :pokemon="selectedPokemon" />
</template>

<style scoped>
@media (min-width: 1024px) {
}
</style>
