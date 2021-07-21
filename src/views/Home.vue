<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      Title:
      <input type="text" v-model="newPostsParams.title" />
      Body:
      <input type="text" v-model="newPostsParams.body" />
      Image:
      <input type="text" v-model="newPostsParams.image" />
      <!-- <img v-bind:src="post.image" alt="post.title" /> -->
    </div>
    <button v-on:click="createPost()">Create a new post!</button>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>Title: {{ post.title }}</h2>
      <p>Body: {{ post.body }}</p>
      <!-- <p>Image: {{ post.image }}</p> -->
      <img v-bind:src="post.image" alt="post.title" />
      <button v-on:click="showPost(post)">More info!</button>
    </div>
    <dialog id="post-details">
      <form method="dialog">
        <h1>Post Info!</h1>
        <p>
          Title:
          <input type="text" v-model="currentPost.title" />
        </p>
        <p>
          Body:
          <input type="text" v-model="currentPost.body" />
        </p>
        <p>
          Image:
          <input type="text" v-model="currentPost.image" />
        </p>
        <button v-on:click="updatePost(currentPost)">Update</button>
        <button v-on:click="destroyPost(currentPost)">Destroy</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to blog-frontend-app!",
      posts: [],
      newPostsParams: {},
      currentPost: {},
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts:", this.posts);
      });
    },
    createPost: function () {
      console.log("Creating post");
      axios
        .post("http://localhost:3000/posts", this.newPostsParams)
        .then((response) => {
          console.log("Success!", response.data);
          this.posts.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showPost: function (post) {
      console.log(post);
      this.currentPost = post;
      document.querySelector("#post-details").showModal();
    },
    updatePost: function (post) {
      var editPostParams = post;
      axios.patch("http://localhost:3000/posts/" + post.id, editPostParams).then((response) => {
        console.log("Success!", response.data);
      });
    },
    destroyPost: function (post) {
      axios.delete("http://localhost:3000/posts/" + post.id).then((response) => {
        console.log("Success!", response.data);
        var index = this.posts.indexOf(post);
        this.posts.splice(index, 1);
      });
    },
  },
};
</script>
