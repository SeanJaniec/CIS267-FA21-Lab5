<template>
  <div id="all">
 
    <div id="all-pokemon">

      <PokemonCard 
        @click-pokemon="add"

        v-for="p in allPokemon" 
        :key="p.id" 
        :pokemon="p" 
        
        />

    </div>
  </div>
</template>

<script>
import PokemonCard from "./PokemonCard.vue"

export default {
  name: "AllPokemon",
  components: {
    PokemonCard
    },
  props: {
    allPokemon: Array,
  },
  methods: {
        add(id) {
      this.$emit("add-pokemon", id);
      console.log(id)
    },

    }
  
};
</script>

<style>

#all-pokemon {
  overflow: scroll;
  height: 50vh;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;

}</style>