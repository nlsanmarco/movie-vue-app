<template>
  <div class="movies-index">
    <div>
      Search by Title:
      <input type="text" v-model="titleFilter" list="titles" />
    </div>
    <br />
    <button v-on:click="sortAttribute = 'title'">Sort by title</button>
    <button v-on:click="sortAttribute = 'year'">Sort by Year</button>

    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <h1>All Movies</h1>

    <!-- <div v-for="movie in movies" v-bind:key="movie.id"> -->
    <!-- <div v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id"> -->
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute)" v-bind:key="movie.id">
      <h2>{{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
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
      sortAttribute: "",
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
