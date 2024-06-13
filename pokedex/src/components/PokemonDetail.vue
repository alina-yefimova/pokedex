<template>
  <div v-if="pokemon">
    <h2>{{ pokemon.name }}</h2>
    <img :src="pokemon.image" alt="{{ pokemon.image }}" />
  </div>
  <p v-else>No Pokemon selected.</p>
</template>

<script>
export default {
  props: {
    pokemon: Object,
  },
};
</script>
