<template>
  <div class="about">
    <div
      v-if="pokemon"
      class="w-3/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center"
    >
      <h3 class="text-2xl text-green-900 uppercase">{{ pokemon.name }}</h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.front_shiny" alt="" />
        <img class="w-48" :src="pokemon.sprites.back_shiny" alt="" />
      </div>
      <h3 class="text=yellow-400">Types</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class="text-blue-900">{{ type.type.name }}</h5>
      </div>
    </div>
  </div>
</template>

<style></style>

<script lang="ts">
import { useRoute } from "vue-router";
import { defineComponent, reactive, toRefs } from "vue";
export default defineComponent({
  setup() {
    const route = useRoute();
    const API = `https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`;
    const state = reactive({
      pokemon: {
        name: "",
        sprites: {
          front_shiny: "",
          back_shiny: "",
        },
        types: {
          type: {
            type: {
              name: "",
            },
          },
        },
      },
    });
    fetch(API)
      .then((response) => response.json())
      .then((data) => {
        state.pokemon = data;
      });
    return { ...toRefs(state) };
  },
});
</script>
