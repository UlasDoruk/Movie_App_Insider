<template>
  <div class="movie-card flex flex-col gap-2">
    <img class="movie-poster shadow-md rounded-lg" :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
      :alt="movie.title" />
    <div class="text-left	p-2 font-bold	text-slate-800 rounded-lg">
      <p class="movie-name text-[16px] mn-h-[40px] font-bold	 text-left">{{ movie.title }}</p>
      <p class="release-date pt-2 text-[12px] pb-2 text-left">{{ movie.release_date }}</p>
      <div class="flex  w-full items-center rounded-lg ">
        <span class="">{{ Math.floor(movie.vote_average) }}</span>
        <button class="ml-1" v-if="showFavoriteButton" @click="toggleFavorite(movie)">
          <span v-if="isFavorited(movie.id)">★</span>
          <span v-else>☆</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  name: 'MovieCard',
  props: {
    movie: {
      type: Object,
      required: true
    },
    showFavoriteButton: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    ...mapGetters(['isFavorited'])
  },
  methods: {
    ...mapActions(['toggleFavorite'])
  }
};
</script>

<style scoped>
.movie-poster {
  width: 100%;
  height: auto;
}

button {
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
}
</style>
