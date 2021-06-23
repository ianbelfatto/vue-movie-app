<template>
  <div class="movies-index">
    <h1>Movie Index</h1>
    Search by Title:
    <input placeholder="Search something..." v-model="titleFilter" />

    <div class="row">
      <div class="col-sm-4" v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
        <div class="card">
          <img :src="movie.image_url" class="card-img-top" alt="" />
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">{{ movie.year }}</p>
            <p>{{ movie.plot }}</p>
            <router-link class="btn btn-info" :to="`/movies/${movie.id}`">Movie Details</router-link>
          </div>
        </div>
      </div>
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
