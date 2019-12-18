<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <button v-on:click="deletePost()">Delete post</button>
    <p>{{ post.title }}</p>
    <p>{{ post.body }}</p>
    <p>{{ post.image }}</p>
    <img v-bind:src="post.image">
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Welcome to the show!",
      post: {}
    };
  },
  created: function() {
    axios.get(`/api/posts/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {
    deletePost: function() {
      console.log("deleting post");
      axios.delete(`/api/posts/${this.$route.params.id}`).then(response => {
        this.$router.push("/posts");
      });
    }
  }
};
</script>
