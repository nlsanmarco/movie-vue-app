<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
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
        <br />
        <small>{{ 200 - newMovieParams.plot.length }} characters remaining</small>
      </div>
      <div>
        Director:
        <input type="text" v-model="newMovieParams.director" />
      </div>
      <div>
        Is the movie in English?
        <br />
        Yes
        <input type="radio" v-model="newMovieParams.english" value="true" />
        No
        <input type="radio" v-model="newMovieParams.english" value="false" />
      </div>
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<style></style>

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
  created: function () {},
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
