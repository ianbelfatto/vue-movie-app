<template>
  <div class="home">
    <h2>Create a Movie</h2>
    Title:
    <input type="text" v-model="newTitle" />
    <br />
    Year:
    <input type="text" v-model="newYear" />
    <br />
    Plot:
    <input type="text" v-model="newPlot" />
    <br />
    <button v-on:click="createMovie()">Add Movie</button>
    <br />
    <div v-for="movie in movies" :key="movie.id">
      <h2>{{ movie.title }}</h2>
      <button v-on:click="showMovie(movie)">More Info</button>
      <!-- <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p> -->
      <br />
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info</h1>
        <img src="" alt="" />
        <p>Title: {{ currentMovie.title }}</p>
        <p>Year: {{ currentMovie.year }}</p>
        <p>Plot: {{ currentMovie.plot }}</p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newTitle: "",
      newYear: "",
      newPlot: "",
      currentMovie: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = {
        title: this.newTitle,
        year: this.newYear,
        plot: this.newPlot,
      };
      axios.post("http://localhost:3000/movies", params).then((response) => {
        this.movies.push(response.data);
        console.log(response.data);
      });
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
  },
};
</script>
