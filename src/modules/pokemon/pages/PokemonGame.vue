<template>
  <section v-if="isLoading || randomPokemon.id === null"
    class="flex flex-col items-center justify-center w-screen h-screen">
    <h1 class="text-3xl">Espere por favor</h1>
    <h3 class="animate-pulse">Cargando Pokemons</h3>
  </section>

  <section v-else class="flex flex-col items-center justify-center w-screen h-screen">
    <h1 class="m-5">¿Quien es este pokemon?</h1>

    <div class="h-20">
      <button class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-700 transition-all"
        v-if="gameStatus !== GameStatus.Playing" @click="getNextRound(4)">
        Jugar de nuevo
      </button>
    </div>
    <!-- Pokemon Picture  -->
    <PokemonPicture :pokemonId="randomPokemon.id" :show-pokemon="gameStatus !== GameStatus.Playing" />

    <!-- Pokemon Options -->
    <PokemonOptions :options="options" :block-selection="gameStatus !== GameStatus.Playing"
      :correct-answer="randomPokemon.id" @selected-option="checkAnswer" />

  </section>
</template>

<script setup lang="ts">
import PokemonOptions from '../components/PokemonOptions.vue';
import PokemonPicture from '../components/PokemonPicture.vue';
import { usePokemonGame } from '../composables/usePokemonGame';
import { GameStatus } from '../interfaces';

const { isLoading, randomPokemon, gameStatus, pokemonOptions: options, checkAnswer, getNextRound } = usePokemonGame();

</script>

<style scoped></style>
