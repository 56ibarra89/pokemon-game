<template>
  <section v-if="false" class="flex flex-col items-center justify-center h-screen">
    <h1 class="text-3xl font-bold">Espere un momento...</h1>
    <h3 class="animate-pulse">Estamos cargando los Pokemons</h3>
  </section>

  <section class="flex flex-col items-center justify-center h-screen">
    <h1>¿quien es este Pokemon?</h1>
    <!-- PokemonPicture -->
    <PokemonPicture />
    <!-- PokemonOptions -->
    <PokemonOptions />
  </section>
</template>

<script lang="ts" setup>
import PokemonPicture from '@/modules/pokemon/components/PokemonPicture.vue';
import PokemonOptions from '@/modules/pokemon/components/PokemonOptions.vue';
</script>
