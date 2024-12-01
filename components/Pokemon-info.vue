<template>
  <div id="pokemon-info">
    <img :src="selectedPokemon.image" alt="Pokemon image" />
    <div id="pokemon-types">
      <span
        v-for="(type, index) in selectedPokemon.type"
        :key="index"
        :class="['type-box', type]"
      >
        {{ type.toUpperCase() }}
      </span>
    </div>
    <div id="pokemon-description">
      {{ selectedPokemon.description }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Pokemon-info",
  props: {
    selectedPokemon: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
#pokemon-info {
  width: 320px;
  height: 100%;
  padding: 20px;
  background-color: #fff;
  text-align: center;
  border-right: 2px solid #ddd;
  transition: transform 0.3s ease-in-out;
}

#pokemon-info img {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  margin-top: 20px;
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease-in-out;
}

#pokemon-info img:hover {
  transform: rotate(15deg);
}

#pokemon-types {
  margin-top: 15px;
}

.type-box {
  padding: 6px 12px;
  margin: 6px;
  border-radius: 20px;
  display: inline-block;
  font-weight: bold;
  font-size: 14px;
  color: #fff;
  transition: transform 0.2s ease, background-color 0.3s ease;
}

.type-box:hover {
  transform: scale(1.1);
}

#pokemon-description {
  width: 260px;
  height: 120px;
  background-color: #fff;
  border-radius: 10px;
  padding: 10px;
  margin: 20px auto;
  border: 1px solid #ddd;
  font-size: 16px;
  color: #555;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  overflow-y: auto;
}

#pokemon-description::-webkit-scrollbar {
  width: 6px;
}

#pokemon-description::-webkit-scrollbar-thumb {
  background-color: #ccc;
  border-radius: 10px;
}
</style>