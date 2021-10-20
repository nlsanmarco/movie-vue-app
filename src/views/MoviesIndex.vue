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

    <div class="row row-cols-1 row-cols-md-3 g-4">
      <div
        class="col"
        v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute)"
        v-bind:key="movie.id"
      >
        <div class="card" style="width: 18rem">
          <img
            src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcdn.quotesgram.com%2Fsmall%2F67%2F98%2F188724369-98be691c2e4ab2d9487a423f9e805cce.jpg&f=1&nofb=1"
            class="card-img-top"
            alt="..."
          />
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">
              Year: {{ movie.year }}
              <br />
              Plot: {{ movie.plot }}
              <br />
              Director: {{ movie.director }}
            </p>
            <router-link :to="`/movies/${movie.id}`" class="btn btn-outline-secondary">See Details</router-link>
          </div>
        </div>
      </div>
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
