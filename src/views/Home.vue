<template>
  <div class="container my-4">
    <input
      class="form-control border-primary rounded-pill text-center mb-5"
      v-model="search"
      placeholder="Search Pokemons"
      >
    <div class="row justify-content-center">
      <div
        v-for="(pokemon, idx) in filteredPokemons"
        :key="pokemon.name"
        class="col-xl-2 col-md-4 col-sm-6 col-12 my-2"
        >
        <div class="card border-primary text-dark text-center">
          <div class="card-body p-3">
            <router-link :to="{ name: 'about.pokemon', params : { pokemon: pokemon.name }}" v-text="pokemon.name" class="text-decoration-none"/>
          </div>
        </div>
      </div>
    </div>
    <div class="row justify-content-center py-3">
        <button
          class="btn btn-primary col-4 me-2"
          :disabled="state.prevPage == null"
          @click="loadPage(state.prevPage)"
          >
        Previous Page
        </button>
        <button
          class="btn btn-primary col-4"
          :disabled="state.nextPage == null"
          @click="loadPage(state.nextPage)"
          >
        Next Page
        </button>
      </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, computed } from 'vue';

const search = ref('');
const api = ref('https://pokeapi.co/api/v2/pokemon/?offset=0')
const state = reactive({
  pokemons: [],
  nextPage: null,
  prevPage: null
});

const fetchPokemons = async () => {
  try {
    const response = await fetch(api.value);
    const data = await response.json();
    state.pokemons = data.results;
    state.nextPage = data.next;
    state.prevPage = data.previous;
  } catch (error) {
    console.error('Error fetching pokemons:', error);
  }
};

onMounted(() => {
  fetchPokemons();
});

const filteredPokemons = computed(() => {
  return state.pokemons.filter(pokemon =>
    pokemon.name.toLowerCase().includes(search.value.toLowerCase())
  );
});

const loadPage = (newApi) => {
  api.value = newApi;
  fetchPokemons();
}
</script>
