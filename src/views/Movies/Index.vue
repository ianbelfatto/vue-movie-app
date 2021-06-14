<template>
  <div class="movies-index">
    <input type="text" v-model="titleFilter" placeholder="Search" />
    <div v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
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
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
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
