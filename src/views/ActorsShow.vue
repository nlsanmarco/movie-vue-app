<template>
  <div class="actors-show">
    <div>
      <h2>Actor: {{ actor.first_name }} {{ actor.last_name }}</h2>
      <p>Known For: {{ actor.known_for }}</p>
      <p>Gender: {{ actor.gender }}</p>
      <p>Age: {{ actor.age }}</p>
    </div>
    <router-link :to="`/actors/${actor.id}/edit`">Edit</router-link>
    <br />
    <button v-on:click="destroyActor()">Delete</button>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      actor: {},
    };
  },
  created: function () {
    axios.get(`/actors/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.actor = response.data;
    });
  },
  methods: {
    destroyActor: function () {
      axios.delete(`/actors/${this.actor.id}`).then((response) => {
        console.log(response.data);
        this.$router.push("/actors");
      });
    },
  },
};
</script>
