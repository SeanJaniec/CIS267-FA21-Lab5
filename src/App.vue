<template>
  <nav>NAVIGATION</nav>

  <PartyPokemon 
    :partyPokemon="partyPokemon"
    @remove-pokemon="remove"
    />

    <FilterPokemon 
    :filterPokemon="filterPokemon"
    @add-pokemon="add"
    />

    <AllPokemon 
    :allPokemon="allPokemon"
    @add-pokemon="add"
    />



  <footer> &copy; 2021 </footer>
</template>

<script>

const getPokemon = async function (id) {
    // get pokemon data from pokeapi
    const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
  
    const response = await fetch(url);
    const data = await response.json();
  
    return data;
    //createPokemonCard( data );
  };

// import HelloWorld from './components/HelloWorld.vue'
import PartyPokemon from "./components/PartyPokemon.vue"
import AllPokemon from "./components/AllPokemon.vue"
import FilterPokemon from "./components/FilterPokemon.vue"
export default {
  name: 'App',
  components: {
    PartyPokemon,
    AllPokemon, 
    FilterPokemon
  },
  data() {
    return {
      pp: [
        {name:"Charmader", id: 3},
        {name:"Bulbasaur", id: 2},
        {name:"Pikachu", id: 4}
        ],
      allPokemon: [

      ],
      partyPokemon: [],
      filteredPokemon: [],


    }
  },
  methods: {
    remove(id) {
      this.partyPokemon = this.partyPokemon.filter( p => p.id!= id);
    },
    add(id) {
      if(this.partyPokemon.length < 6){
        //let pokemon = this.allPokemon.filter( p => p.id == id) 
          this.allPokemon.forEach( p => {
            if(p.id == id){
              let pokemon = p;
                      console.log(pokemon);
        const pokemonCopy = {...pokemon};
        pokemonCopy.guid = this.getGUID();
        console.log(pokemonCopy.guid);
        this.partyPokemon.push(  pokemonCopy );
            }
      });
        
        
      }
    },
        getGUID() {
      return Math.floor(Math.random()* 1000000);
    },

    async loadAllPokemon() {
      //load all pokemon from API
      const pokemon_count = 20;
      let pokemon = [];
      for (let i = 1; i <= pokemon_count; i++) {
        let p = await getPokemon(i);
        if (p.name === "mr-mime") {
          p.name = "Mr. Mime";
        }
        p.isFavorite = false;

        pokemon.push(p);
      }

      pokemon.forEach( p => {
          this.allPokemon.push(p);
            console.log(p);
      });
      
    }
  },

    mounted() {
    this.loadAllPokemon();
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
