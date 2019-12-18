<template>
  <div class="posts-index">
    <h1>{{ message }}</h1>

    <div v-for="post in posts">
      <p>{{ post.title }}</p>
      <p>{{ post.body }}</p>
      <img v-bind:src="post.image">
      <br>
      <router-link v-bind:to="`/posts/${post.id}`">Show page</router-link>
      <hr>
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Welcome to the Posts page!",
      posts: []
    };
  },
  created: function() {
    axios.get("/api/posts").then(response => {
      console.log(response.data);
      this.posts = response.data;
    });
  },
  methods: {}
};
</script>