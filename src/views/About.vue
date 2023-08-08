<template>
  <div class="container my-4">
    <div class="card card-sm">
      <h5 class="card-title text-center fw-bold">
        {{ pokemonInfo.name.charAt(0).toUpperCase() + pokemonInfo.name.slice(1) }}
      </h5>
      <div class="d-flex justify-content-center">
        <img :src="pokemonInfo.sprites.front_shiny" alt="" class="">
        <img :src="pokemonInfo.sprites.back_shiny" alt="" class="">
      </div>
      <div class="card-body">
        <div class="row d-flex justify-content-evenly">
          <div class="col-xl-2 col-md-4 col-sm-6 col-12 my-2 card">
            <ul><b>Ability</b>
              <li v-for="(val, idx) in pokemonInfo.abilities">
                {{ val.ability.name }}
              </li>
            </ul>
          </div>
          <div class="col-xl-2 col-md-4 col-sm-6 col-12 my-2 card">
            <ul><b>Types</b>
              <li v-for="(val, idx) in pokemonInfo.types">
                {{ val.type.name }}
              </li>
            </ul>
          </div>
          <div class="col-xl-2 col-md-4 col-sm-6 col-12 my-2 card">
            <ul><b>Stats</b>
              <li v-for="(val, idx) in pokemonInfo.stats">
                {{ val.stat.name }}
              </li>
            </ul>
          </div>
          <div class="d-flex">
            <button class="btn btn-primary m-auto mt-5"
            @click="$router.go(-1)">
              Back
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { useRoute } from 'vue-router';
import { onBeforeMount, ref } from 'vue';

const route = useRoute();
const pokemonInfo = ref({});

const fetchPokemon = () => {

  fetch('https://pokeapi.co/api/v2/pokemon/' + route.params.pokemon)
    .then((resp) => resp.json())
    .then((data) => {
      pokemonInfo.value = data;
    })
}

onBeforeMount(() =>{
  fetchPokemon();
})
</script>