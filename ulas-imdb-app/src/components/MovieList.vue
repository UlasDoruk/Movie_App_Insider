<template>
  <div>
    <div class="search-bar-container bg-blue-500 text-white p-4 ">
      <h2 class="bg-blue-500 text-white p-4 bg-blue-900	font-bold	font-mono text-white rounded mr-4 ml-4 h-1/2">Film
        List</h2>
      <input type="text" v-model="searchQuery" placeholder="Search for a movie..."
        class="search-bar text-left	 block w-4/5 p-4 ps-10 text-sm text-black border border-white-300 bg-white-50  dark:border-grey-600 dark:placeholder-white-400 dark:text-black" />
      <button class="hidden">Search</button>
    </div>
    <ul>
      <li class="min-h-[450px] w-[300px] mt-[10px] mb-[10px]" v-for="item in filteredMovies" :key="item.id">
        <MovieCard :movie="item" showFavoriteButton />
      </li>
    </ul>
  </div>
</template>


<script>
import { ref, computed } from 'vue';
import axios from 'axios';
import MovieCard from './MovieCard.vue';
import { mapActions } from 'vuex';

export default {
  name: 'MovieList',
  components: {
    MovieCard
  },
  setup() {
    const movies = ref([]);
    const searchQuery = ref('');

    const fetchMovies = () => {
      const url = `https://api.themoviedb.org/3/movie/top_rated?api_key=348088421ad3fb3a9d6e56bb6a9a8f80`;

      axios.get(url)
        .then(response => {
          movies.value = response.data.results;
        })
        .catch(error => {
          console.error(error);
        });
    };

    const filteredMovies = computed(() => {
      if (searchQuery.value.length < 3) {
        return movies.value;
      }
      return movies.value.filter((movie) =>
        movie.title.toLowerCase().includes(searchQuery.value.toLowerCase())
      );
    });

    return {
      movies,
      searchQuery,
      filteredMovies,
      ...mapActions(['toggleFavorite']),
      fetchMovies
    };
  },
  mounted() {
    this.fetchMovies();
  }
};
</script>

<style>
* {
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  align-items: center;
}

.relase-date {
  font-size: 12px;
  color: #666;
}

.movie-poster {
  width: 100%;
  height: auto;
}

.movie-name {
  font-size: 16px;
  font-weight: bold;
  min-height: 40px;
}

.search-bar-container {
  display: flex;
}

.search-bar {
  width: 30%;
  padding: 10px;
  margin-bottom: 20px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>
