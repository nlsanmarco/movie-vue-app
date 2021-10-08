<template>
  <div class="actors-new">
    <form v-on:submit.prevent="createActor()">
      <h1>New Actor</h1>
      <div>
        First Name:
        <input type="text" v-model="newActorParams.first_name" />
      </div>
      <div>
        Last Name:
        <input type="text" v-model="newActorParams.last_name" />
      </div>
      <div>
        Known For:
        <input type="text" v-model="newActorParams.known_for" />
      </div>
      <div>
        Gender:
        <input type="text" v-model="newActorParams.gender" />
      </div>
      <div>
        Age:
        <input type="text" v-model="newActorParams.age" />
      </div>
      <div>
        Movie Id:
        <input type="text" v-model="newActorParams.movie_id" />
      </div>
      <input type="submit" value="Create" />
      <br />

      newActorParams: {{ newActorParams }}
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      errors: [],
      newActorParams: {},
    };
  },

  methods: {
    createActor: function () {
      axios
        .post("/actors", this.newActorParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/actors");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
