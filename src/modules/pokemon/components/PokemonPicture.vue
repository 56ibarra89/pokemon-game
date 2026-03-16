<template>
  <section class="mb-4 sm:mb-6 w-full flex justify-center">
    <!-- Unrevealed Pokemon: Silhouette with floating effect and dark contrast -->
    <img v-if="!showPokemon" :src="pokemonImage" class="brightness-0 h-[180px] sm:h-[220px] filter drop-shadow-[0_10px_10px_rgba(0,0,0,0.8)] animate-pulse-slow" draggable="false" />
    
    <!-- Revealed Pokemon: Full color with pop animation -->
    <img v-else :src="pokemonImage" class="h-[180px] sm:h-[220px] filter drop-shadow-[0_20px_20px_rgba(255,255,255,0.1)] pokemon-pop relative z-10" alt="pokemon image" draggable="false" />
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  pokemonId: number;
  showPokemon?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  showPokemon: false,
});

const pokemonImage = computed(
  () =>
    `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${props.pokemonId}.svg`,
);
</script>

<style scoped>
img {
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
  transform-origin: bottom center;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}
.animate-pulse-slow {
  animation: float 3s ease-in-out infinite;
}

@keyframes pop {
  0% { transform: scale(0.85) translateY(10px); opacity: 0; filter: blur(5px); }
  50% { transform: scale(1.1) translateY(-5px); filter: blur(0px); }
  100% { transform: scale(1) translateY(0); opacity: 1; filter: blur(0px); }
}
.pokemon-pop {
  animation: pop 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}
</style>
