<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link :to="`/movies/${movie.id}`">
        <h2>{{ movie.title }}</h2>
      </router-link>

      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log("movies array", response.data);
      this.movies = response.data;
    });
  },
};
</script>
