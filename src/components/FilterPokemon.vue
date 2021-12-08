<template>
  <div id="filter">
 
    <div id="filter-pokemon">

      <PokemonCard 
        v-for="p in filterPokemon" 
        :key="p.id" 
        :pokemon="p" 
        
        @click-pokemon="add"
        />

    </div>
  </div>
</template>

<script>
import PokemonCard from "./PokemonCard.vue"

export default {
  name: "FilterPokemon",
  components: {
    PokemonCard
    },
  props: {
    filterPokemon: Array,
  },
  methods: {
    add(id) {
      this.$emit("filter-pokemon", id);
    }
  }
};
</script>

<style></style>