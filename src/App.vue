<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="bg-dark vh-100">
    <div class="fs-1 text-center pt-5 fw-semibold text-light">
        Pokemon Picker
    </div>
    <RouterView />
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@1,500&display=swap');
* {
  font-family: 'Montserrat', sans-serif;
}
</style>
