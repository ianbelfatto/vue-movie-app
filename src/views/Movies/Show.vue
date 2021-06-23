<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <p>{{ movie.year }}</p>
    <p>{{ movie.plot }}</p>
    <router-link class="btn btn-primary" to="/movies" tag="button">Back to All Movies</router-link>
    |
    <router-link class="btn btn-secondary" :to="`/movies/${movie.id}/edit`">Edit Movie</router-link>
    |
    <button class="btn btn-warning" v-on:click="destroyMovie()">Delete Movie</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },

  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log("movies Object", response.data);
      this.movie = response.data;
    });
  },

  methods: {
    destroyMovie: function () {
      if (confirm("Are you sure?\nClick OK to delete!")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
