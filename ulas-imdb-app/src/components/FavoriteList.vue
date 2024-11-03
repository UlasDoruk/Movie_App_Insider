<template>
  <div class="flex items-center justify-center flex-col	gap-y-5">
    <h2 class="flex items-center justify-center text-slate-900 font-bold rounded-lg text-nowrap p-3 mt-5 bg-sky-200">
      <span>Favorite Movies</span>
      <span class="text-stone-100 rounded-sm	p-[10px] ml-[10px] bg-sky-900">{{ favorites.length }}</span>
    </h2>
    <ul>
      <li class="" v-for="item in favorites" :key="item.id">
        <MovieCard :movie="item" />
      </li>
    </ul>
  </div>
</template>

<script>
import { computed } from 'vue';
import { useStore } from 'vuex';
import MovieCard from './MovieCard.vue';

export default {
  name: 'FavoriteList',
  components: {
    MovieCard
  },
  setup() {
    const store = useStore();

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
