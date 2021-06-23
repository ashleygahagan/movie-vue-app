<template>
  <div class="movies-index">
    <input type="text" v-model="titleFilter" placeholder="Search" />
    <div class="container">
      <br />
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div class="col" v-for="movie in filterBy(movies, filter, 'title', 'director')" v-bind:key="movie.id">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }}</h5>
              <p class="card-text">
                {{ movie.plot }}
                <br />
                Year: {{ movie.year }}
                <br />
                Director: {{ movie.director }}
              </p>
              <router-link :to="`/movies/${movie.id}`">
                <button type="button" class="btn btn-outline-primary btn-sm">More Detail</button>
              </router-link>
            </div>
          </div>
        </div>
      </div>
      <!-- <div v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <router-link :to="`/movies/${movie.id}`">More Info</router-link>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p> -->
    </div>
  </div>
</template>

<style></style>

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
      console.log(response.data);
      this.movies = response.data;
    });
  },
};
</script>
