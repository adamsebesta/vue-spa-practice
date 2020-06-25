<template>
  <div id="app">
    <header>
      <h1>Vue.js SPA</h1>
    </header>
    <main>
      <aside class="sidebar">
        <router-link
          :key="post.title"
          v-for="post in posts"
          class="link"
          :to="{ name: 'post', params: { id: post.id } }">
          {{post.id}}. {{ post.title }}
        </router-link>
      </aside>
      <div class="content">
        <router-view></router-view>
      </div>
    </main>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';

export default {
  props: ['id'],
  data() {
    return {
      posts: [],
      endpoint: 'https://jsonplaceholder.typicode.com/posts/',
    };
  },

  created() {
    this.getAllPosts();
  },

  methods: {
    getAllPosts() {
      axios.get(this.endpoint)
        .then((response) => {
          this.posts = response.data;
        });
    },
  },
};
</script>

<style>
  body {
    margin: 0;
    padding: 0;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }
  h1, h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  header {
    position: fixed;
    top: 0;
    width: 100%;
    min-height: 90px;
    border-bottom: 1px solid #42b983;
    text-align: center;
    background: #ffffff;
  }
  main {
    display: flex;
    height: calc(100vh - 90px);
    max-width: 1200px;
    margin-top: 90px;
    margin-left: auto;
    margin-right: auto;
    overflow: hidden;
  }
  aside {
    flex: 1 0 30%;
    height: 100%;
    overflow-y: auto;
    width: 30%;
    padding: 50px 30px;
    box-sizing: border-box;
    border-right: 1px solid #42b983;
  }
  .content {
    flex: 1 1 70%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .link {
    display: block;
    text-decoration: none;
    margin-bottom: 10px;
    color: #2c3e50;
  }
  .link --home {
    text-transform: uppercase;
    margin-bottom: 30px;
  }
  .link .is-active {
    color: #42b983;
  }
</style>
