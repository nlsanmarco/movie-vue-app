<template>
  <div class="movies-new">
    <h1>New Movie</h1>
    <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
    </div>
    <div>
      Year:
      <input type="text" v-model="newMovieParams.year" />
    </div>
    <div>
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
    </div>
    <div>
      Director:
      <input type="text" v-model="newMovieParams.director" />
    </div>
    <div>
      <input type="text" />
    </div>
    <div><button v-on:click="createMovie()">Create</button></div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: {},
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      axios
        .post("http://localhost:3000/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.movies.push(response.data);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
