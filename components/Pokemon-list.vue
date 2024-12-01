<template>
  <div id="pokemon-list">
    <div
      v-for="(pokemon, index) in pokemons"
      :key="index"
      class="pokemon-name"
      @click="selectPokemon(pokemon)"
    >
      {{ index + 1 + "." + " " + pokemon.name.toUpperCase() }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Pokemon-list",
  props: {
    pokemons: {
      type: Array,
      required: true,
    },
  },
  methods: {
    selectPokemon(pokemon) {
      this.$emit("pokemon-selected", pokemon);
    },
  },
};
</script>

<style scoped>
#pokemon-list {
  width: 280px;
  height: 100%;
  padding: 20px;
  font-size: 16px;
  overflow-y: auto;
  background-color: #f7f7f7;
  border-left: 2px solid #ddd;
}

.pokemon-name {
  background-color: #fff;
  color: #333;
  border: 1px solid #ddd;
  border-radius: 12px;
  padding: 8px;
  margin: 8px 0;
  cursor: pointer;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s, box-shadow 0.3s;
}

.pokemon-name:hover {
  background-color: #f0f0f0;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}
</style>