<template>
  <div class="flex items-center justify-center flex-col	gap-y-5">
    <h2 class="flex items-center justify-center text-white rounded-lg text-nowrap p-3 mt-5 bg-sky-300">Favorite Movies</h2>
    <h1 class="text-white rounded w-24 bg-sky-300">{{ favorites.length }}</h1>
    <ul>
      <li v-for="item in favorites" :key="item.id">
        <MovieCard :movie="item" />
      </li>
    </ul>
  </div>
</template>

<script>
import { computed } from 'vue';
import { useStore } from 'vuex'; // Import useStore
import MovieCard from './MovieCard.vue';

export default {
  name: 'FavoriteList',
  components: {
    MovieCard
  },
  setup() {
    const store = useStore(); // Get the Vuex store

    // Access the Vuex state using the store
    const favorites = computed(() => store.getters.favorites);

    return {
      favorites
    };
  }
};
</script>

<style scoped>
/* Styles here */
</style>
