<template>
  <div class="home">
    <h2>New Movie</h2>
    Title:
    <input type="text" v-model="movieTitle" />
    <br />
    Year:
    <input type="text" v-model="movieYear" />
    <br />
    Plot:
    <input type="text" v-model="moviePlot" />
    <br />
    Director:
    <input type="text" v-model="movieDirector" />
    <br />
    <button v-on:click="createMovie()">Create Movie</button>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h3>Title: {{ movie.title }}</h3>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>Title: {{ currentMovie.title }}</p>
        <p>Year: {{ currentMovie.year }}</p>
        <p>Director: {{ currentMovie.director }}</p>
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
      currentMovie: "",
      movieTitle: "",
      movieYear: "",
      movieDirector: "",
      moviePlot: "",
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
        title: this.movieTitle,
        year: this.movieYear,
        plot: this.moviePlot,
        director: this.movieDirector,
      };
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          console.log("Success!", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => {
          console.log(error.response);
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
