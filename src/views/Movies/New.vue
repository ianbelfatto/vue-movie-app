<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="newMovieParams.title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="newMovieParams.year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="newMovieParams.plot" />
      </div>
      <small v-if="newMovieParams.plot.length < 101">
        Character's Remaining: {{ 100 - newMovieParams.plot.length }}
      </small>
      <small v-if="newMovieParams.plot.length > 100" class="text-danger">Cannot be greater than 100 characters!</small>
      <br />
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
    newMovieParams: {{ newMovieParams }}
  </div>
</template>

<style scoped>
.text-danger {
  color: red;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newMovieParams: {
        plot: "",
      },
      errors: [],
    };
  },
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
