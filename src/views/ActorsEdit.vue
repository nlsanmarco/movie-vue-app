<template>
  <div class="actors-edit">
    <form v-on:submit.prevent="editActor()">
      <h1>Edit Actor</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        First Name:
        <input type="text" v-model="editActorParams.first_name" />
      </div>
      <div>
        Last Name:
        <input type="text" v-model="editActorParams.last_name" />
      </div>
      <div>
        Known For:
        <input type="text" v-model="editActorParams.known_for" />
      </div>
      <div>
        Gender:
        <input type="text" v-model="editActorParams.gender" />
      </div>
      <div>
        Age:
        <input type="text" v-model="editActorParams.age" />
      </div>
      <div>
        Movie Id:
        <input type="text" v-model="editActorParams.movie_id" />
      </div>
      <input type="submit" value="Update" />
    </form>
    editActorParams: {{ editActorParams }}
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editActorParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/actors/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.editActorParams = response.data;
    });
  },
  methods: {
    editActor: function () {
      axios
        .patch(`/actors/${this.editActorParams.id}`, this.editActorParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/actors/${response.data.id}`);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
