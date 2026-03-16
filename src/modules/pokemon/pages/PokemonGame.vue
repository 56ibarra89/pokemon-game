<template>
  <section v-if="isLoading" class="flex flex-col items-center justify-center p-5 mt-5">
    <h1 class="text-3xl font-bold">Espere un momento...</h1>
    <h3 class="animate-pulse">Cargando Pokémons</h3>
  </section>

  <section v-else class="flex flex-col items-center justify-center mt-5">
    <div class="mb-5 flex flex-col items-center">
      <h1 class="text-3xl font-bold">¿Quién es este Pokémon?</h1>
      <h3 class="text-xl">Victorias: {{ countWins }} | Récord: {{ highScore }}</h3>
    </div>

    <!-- Pokemon Picture -->
    <PokemonPicture
      :pokemon-id="randomPokemon?.id!"
      :show-pokemon="gameStatus !== GameStatus.Playing"
    />

    <!-- Pokemon Options -->
    <PokemonOptions
      :options="pokemonOptions"
      :block-selection="gameStatus !== GameStatus.Playing"
      :correct-answer="randomPokemon?.id!"
      :game-status="gameStatus"
      :lives="lives"
      @selected-option="checkAnswer"
    />

    <button
      v-if="gameStatus !== GameStatus.Playing"
      @click="getNextRound()"
      class="mt-5 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
    >
      Siguiente ronda
    </button>
  </section>
</template>

<script lang="ts" setup>
import PokemonPicture from '@/modules/pokemon/components/PokemonPicture.vue';
import PokemonOptions from '@/modules/pokemon/components/PokemonOptions.vue';
import { usePokemonGame } from '../composables/usePokemonGame';
import { GameStatus } from '../interfaces';

const {
  randomPokemon,
  isLoading,
  gameStatus,
  pokemonOptions,
  countWins,
  highScore,
  lives,
  checkAnswer,
  getNextRound,
} = usePokemonGame();
</script>
