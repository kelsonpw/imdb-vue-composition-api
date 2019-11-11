<template>
  <div class="App">
    <Header :title="'Composition API'" />
    <Search :search="state.search" @search="handleSearch" />
    <p class="App-intro">Sharing a few of our favourite movies</p>
    <div class="movies">
      <Movie v-for="movie in state.movies" :movie="movie" :key="movie.imdbID" />
    </div>
  </div>
</template>

<script>
import { reactive, watch } from '@vue/composition-api';
import Header from './components/Header.vue';
import Search from './components/Search.vue';
import Movie from './components/Movie.vue';

const API_KEY = 'a5549d08';

export default {
  name: 'app',
  components: { Header, Search, Movie },
  setup() {
    const state = reactive({
      search: 'Joker',
      loading: true,
      movies: [],
      errorMessage: null,
    });

    watch(() => {
      const MOVIE_API_URL = `https://www.omdbapi.com/?s=${state.search}&apikey=${API_KEY}`;

      fetch(MOVIE_API_URL)
        .then(res => res.json())
        .then(jsonRes => {
          state.movies = jsonRes.Search;
          state.loading = false;
        });
    });

    const handleSearch = search => {
      state.loading = true;
      state.search = search;
    };

    return {
      state,
      handleSearch,
    };
  },
};
</script>
