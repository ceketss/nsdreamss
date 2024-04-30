<template>
    <div class="container">
      <div>
        <h1 class="title">My Blog</h1>
      </div>
      <div class="posts">
        <div v-for="post in posts" :key="post._id">
          <h2><a v-bind:href="post.slug.current" v-text="post.title" /></h2>
        </div>
      </div>
    </div>
  </template>
  
  <script>
    import { groq } from '@nuxtjs/sanity';
  
    export default {
      async asyncData({ $sanity }) {
        const query = groq`*[_type == "post"]`;
        const posts = await $sanity.fetch(query);
        return { posts };
      },
    };
  </script>
  
  <style>
    .container {
      margin: 2rem;
      min-height: 100vh;
    }
    .posts {
      margin: 2rem 0;
    }
  </style>