<template>
  <main class="min-h-screen w-full font-sans bg-slate-900 bg-[radial-gradient(ellipse_at_top,var(--tw-gradient-stops))] from-blue-900 via-slate-900 to-black text-white relative overflow-hidden flex flex-col justify-center items-center selection:bg-blue-500/30">
    
    <!-- Light particles/stars effect (CSS ONLY) -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute w-96 h-96 bg-blue-500/10 rounded-full blur-3xl -top-20 -left-20 animate-pulse" style="animation-duration: 4s;"></div>
      <div class="absolute w-80 h-80 bg-purple-500/10 rounded-full blur-3xl bottom-10 -right-20 animate-pulse" style="animation-duration: 5s; animation-delay: 1s;"></div>
    </div>

    <!-- Loading State -->
    <section
      v-if="isLoading || randomPokemon?.id === null || randomPokemon?.id === undefined"
      class="flex flex-col justify-center items-center z-10"
    >
      <div class="relative w-24 h-24 mb-6 animate-bounce">
        <div class="absolute inset-0 bg-red-500 rounded-t-full border-4 border-slate-800 border-b-8"></div>
        <div class="absolute inset-0 top-1/2 bg-white rounded-b-full border-4 border-slate-800 border-t-0"></div>
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-6 h-6 bg-white border-4 border-slate-800 rounded-full shadow-inner"></div>
      </div>
      <h1 class="text-3xl font-bold tracking-tight text-transparent bg-clip-text bg-linear-to-r from-blue-400 to-emerald-400">Preparando arena...</h1>
    </section>

  <section v-else class="flex flex-col justify-center items-center w-full z-10 p-4 relative min-h-screen">
    <!-- Top Bar: Lives (Left) & Score (Right) -->
    <div class="absolute top-4 left-4 sm:top-6 sm:left-6 flex items-center gap-1.5 bg-slate-800/40 px-4 py-2 rounded-full shadow-[0_8px_32px_0_rgba(0,0,0,0.36)] backdrop-blur-xl border border-white/10 z-10">
      <!-- Pokeball Lives Loop -->
      <template v-for="i in 3" :key="i">
        <svg v-if="i <= lives" viewBox="0 0 100 100" class="w-6 h-6 sm:w-8 sm:h-8 drop-shadow-md transition-transform hover:scale-110" xmlns="http://www.w3.org/2000/svg">
          <!-- Top Red Half -->
          <path d="M 50 5 A 45 45 0 0 1 95 50 L 70 50 A 20 20 0 0 0 30 50 L 5 50 A 45 45 0 0 1 50 5 Z" fill="#ef4444" stroke="#1e293b" stroke-width="4"/>
          <!-- Bottom White Half -->
          <path d="M 50 95 A 45 45 0 0 0 95 50 L 70 50 A 20 20 0 0 1 30 50 L 5 50 A 45 45 0 0 0 50 95 Z" fill="#f8fafc" stroke="#1e293b" stroke-width="4"/>
          <!-- Center Button -->
          <circle cx="50" cy="50" r="14" fill="#f8fafc" stroke="#1e293b" stroke-width="4"/>
          <circle cx="50" cy="50" r="6" fill="#1e293b"/>
          <!-- Highlight (Optional Polish) -->
          <path d="M 30 20 A 30 30 0 0 1 65 10" fill="none" stroke="rgba(255,255,255,0.4)" stroke-width="3" stroke-linecap="round"/>
        </svg>

        <svg v-else viewBox="0 0 100 100" class="w-6 h-6 sm:w-8 sm:h-8 drop-shadow-md opacity-30 grayscale transition-opacity duration-300" xmlns="http://www.w3.org/2000/svg">
          <!-- Top Gray Half -->
          <path d="M 50 5 A 45 45 0 0 1 95 50 L 70 50 A 20 20 0 0 0 30 50 L 5 50 A 45 45 0 0 1 50 5 Z" fill="#64748b" stroke="#0f172a" stroke-width="4"/>
          <!-- Bottom Gray-ish Half -->
          <path d="M 50 95 A 45 45 0 0 0 95 50 L 70 50 A 20 20 0 0 1 30 50 L 5 50 A 45 45 0 0 0 50 95 Z" fill="#cbd5e1" stroke="#0f172a" stroke-width="4"/>
          <!-- Center Button -->
          <circle cx="50" cy="50" r="14" fill="#cbd5e1" stroke="#0f172a" stroke-width="4"/>
          <circle cx="50" cy="50" r="6" fill="#0f172a"/>
        </svg>
      </template>
    </div>

    <!-- Score Card (Glassmorphism) -->
    <div class="absolute top-4 right-4 sm:top-6 sm:right-6 flex flex-col items-end bg-slate-800/40 px-5 py-3 rounded-2xl shadow-[0_8px_32px_0_rgba(0,0,0,0.36)] backdrop-blur-xl border border-white/10 z-10 transition-all hover:bg-slate-800/60 w-36 sm:w-auto">
      <div class="flex items-center gap-2">
        <span class="relative flex h-3 w-3">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
          <span class="relative inline-flex rounded-full h-3 w-3 bg-emerald-500"></span>
        </span>
        <h2 class="text-sm sm:text-base font-bold text-slate-200 tracking-wide uppercase">
          Racha: <span class="text-emerald-400 text-lg sm:text-xl">{{ countWins }}</span>
        </h2>
      </div>
      <h3 class="text-xs sm:text-sm font-medium text-slate-400 mt-1 flex items-center gap-1">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-amber-400" viewBox="0 0 20 20" fill="currentColor">
          <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
        </svg>
        Récord: <span class="text-white font-bold ml-1">{{ highScore }}</span>
      </h3>
    </div>

    <!-- Title Area -->
    <div class="text-center mt-6 sm:mt-4 mb-2 z-10 flex flex-col items-center">
      <h1 class="text-3xl sm:text-4xl font-extrabold text-transparent bg-clip-text bg-linear-to-br from-white to-slate-400 drop-shadow-lg tracking-tight mb-1">
        ¿Quién es este Pokémon?
      </h1>
      <p class="text-slate-400 text-xs sm:text-sm font-medium">Demuestra que eres un maestro Pokémon</p>
    </div>

    <!-- Main Game Components -->
    <div class="relative w-full max-w-lg mx-auto bg-slate-800/30 p-2 sm:p-4 rounded-3xl backdrop-blur-md border border-slate-700/50 shadow-2xl z-10 flex flex-col items-center text-center">
      <PokemonPicture
        :pokemon-id="randomPokemon?.id ?? 0"
        :show-pokemon="gameStatus !== GameStatus.Playing"
      />

      <PokemonOptions
        :options="options"
        :block-selection="gameStatus !== GameStatus.Playing"
        :correct-answer="randomPokemon?.id ?? 0"
        :game-status="gameStatus"
        :lives="lives"
        @selected-option="checkAnswer"
      />
    </div>

    <!-- Play Again Button Container (Moved to bottom) -->
    <div class="h-14 mt-4 mb-1 flex items-center justify-center w-full z-20">
      <transition enter-active-class="transition ease-out duration-300" enter-from-class="transform opacity-0 scale-95 translate-y-4" enter-to-class="transform opacity-100 scale-100 translate-y-0" leave-active-class="transition ease-in duration-200" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
        <button
          v-if="gameStatus !== GameStatus.Playing"
          @click="getNextRound(4)"
          class="group relative inline-flex items-center justify-center px-6 py-2.5 text-sm font-bold text-white transition-all duration-200 bg-blue-600 border border-transparent rounded-full hover:bg-blue-500 hover:shadow-[0_0_20px_rgba(59,130,246,0.6)] focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-600 focus:ring-offset-slate-900 active:scale-95 z-20 overflow-hidden"
        >
          <span class="absolute w-0 h-0 transition-all duration-500 ease-out bg-white rounded-full group-hover:w-56 group-hover:h-56 opacity-10"></span>
          <span class="relative flex items-center gap-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z" clip-rule="evenodd" />
            </svg>
            Siguiente Ronda
          </span>
        </button>
      </transition>
    </div>
  </section>
  </main>
</template>

<script setup lang="ts">
import PokemonOptions from '@/modules/pokemon/components/PokemonOptions.vue';
import PokemonPicture from '@/modules/pokemon/components/PokemonPicture.vue';
import { usePokemonGame } from '@/modules/pokemon/composables/usePokemonGame';
import { GameStatus } from '@/modules/pokemon/interfaces';

const {
  randomPokemon,
  isLoading,
  gameStatus,
  pokemonOptions: options,
  countWins,
  highScore,
  lives,
  checkAnswer,
  getNextRound,
} = usePokemonGame();
</script>
