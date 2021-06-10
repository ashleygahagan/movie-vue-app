<template>
  <div class="movies-show">
    <h2>Movie Info</h2>
    <p>Title: {{ movie.title }}</p>
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: { user: {} },
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function () {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
