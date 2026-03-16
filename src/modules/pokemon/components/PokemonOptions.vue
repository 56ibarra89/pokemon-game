<template>
  <section class="mt-2 flex flex-col justify-center items-center w-full">
    <button
      v-for="{ name, id } in options"
      :key="id"
      @click="$emit('selectedOption', id)"
      :class="[
        'w-full sm:w-64 py-3 px-6 m-2 flex justify-center items-center rounded-xl font-bold tracking-wide capitalize transition-all duration-300 border-2 outline-none focus:ring-4 focus:ring-blue-500/50',
        blockSelection 
          ? 'cursor-not-allowed transform-none' 
          : 'cursor-pointer hover:-translate-y-1 hover:shadow-[0_0_15px_rgba(59,130,246,0.5)] active:translate-y-0 active:scale-95 border-slate-600 bg-slate-700/80 text-slate-200 hover:bg-slate-700 hover:border-blue-500',
        {
          'correct': id === correctAnswer && blockSelection,
          'incorrect': id !== correctAnswer && blockSelection,
          'opacity-40 border-slate-800 bg-slate-800': blockSelection && id !== correctAnswer && gameStatus !== undefined, // Dim unselected options
        },
      ]"
      :disabled="blockSelection"
    >
      {{ name }}
    </button>
  </section>
</template>

<script setup lang="ts">
import type { Pokemon, GameStatus } from '../interfaces';

interface Props {
  options: Pokemon[];
  blockSelection: boolean;
  correctAnswer: number;
  gameStatus: GameStatus;
}

defineProps<Props>();

defineEmits<{
  selectedOption: [id: number];
}>();
</script>

<style scoped>
@reference "tailwindcss";

.correct {
  @apply bg-emerald-500 border-emerald-400 text-white shadow-[0_0_25px_rgba(16,185,129,0.7)] z-10 scale-105;
}

@keyframes shakeAndGlow {
  0%, 100% { transform: translateX(0); box-shadow: 0 0 0 rgba(239,68,68,0); }
  25% { transform: translateX(-6px); box-shadow: 0 0 20px rgba(239,68,68,0.8); }
  50% { transform: translateX(6px); box-shadow: 0 0 20px rgba(239,68,68,0.8); }
  75% { transform: translateX(-6px); box-shadow: 0 0 20px rgba(239,68,68,0.8); }
}

.incorrect {
  @apply bg-red-500/90 border-red-400 text-white z-10;
  animation: shakeAndGlow 0.5s ease-in-out forwards;
}
</style>
