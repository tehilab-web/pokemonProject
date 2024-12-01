<template>
  <div id="app">
    <div id="content-box">
      <PokemonInfo :selectedPokemon="selectedPokemon" />
      <PokemonList :pokemons="pokemons" @pokemon-selected="updatePokemon" />
    </div>
  </div>
</template>

<script>
import PokemonInfo from "./components/Pokemon-info.vue";
import PokemonList from "./components/Pokemon-list.vue";
export default {
  name: "App",
  components: {
    PokemonInfo,
    PokemonList,
  },
  data() {
    return{
    pokemonCount: 300,
    pokemons: [],
    selectedPokemon:{
      image: "",
      type: [],
      description: "",
    },
  };
  },
  mounted() {
    this.loadPokemons()
  },

  methods: {
    async loadPokemons() {
      for (let i = 1; i < this.pokemonCount; i++) await this.getPokemon(i);
    },
    async getPokemon(id) {
      const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
      const res = await fetch(url);
      const data = await res.json();
      const pokemonName = data.name;
      const pokemonImg = data.sprites.front_default;
      const pokemonTypes = data.types.map((type) => type.type.name);

      const speciesRes = await fetch(data.species.url);
      const speciesData = await speciesRes.json();
      const pokemonDesc = speciesData.flavor_text_entries[9].flavor_text;

      this.pokemons.push({
        id,
        name: pokemonName,
        image: pokemonImg,
        type: pokemonTypes,
        description: pokemonDesc,
      });
      if(id===1){
        this.selectedPokemon=this.pokemons[0]
      }
    },
    updatePokemon(pokemon){
      this.selectedPokemon=pokemon
    }
  },
};
</script>

<style  scoped>


#content-box {
  width: 600px;
  height: 600px;
  border-radius: 20px;
  overflow: hidden;
  margin: 80px auto;
  display: flex;
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.1);
  background: radial-gradient(circle, rgba(255, 255, 255, 0.8), rgba(0, 0, 0, 0.1));
}
</style>