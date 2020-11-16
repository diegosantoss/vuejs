<template>
  <section id="posts">
    <section class="post_loading" v-if="loading">
      <p>Carregando posts ...</p>
      <span class="spin"></span>
    </section>
    <section class="post_item" v-else v-for="post in posts" v-bind:key="post.title">
      <img alt="" src="../assets/default-img.jpg">  
      <p class="item_title">{{ post.title }}</p>
      <p class="item_body">{{ post.body }}</p>
    </section>
  </section>
</template>

<script>
  import axios from 'axios';

  export default {
    name: "Posts",
    data: function(){
      return {
        posts: [],
        loading: true
      }
    },
    mounted: function(){
      axios.get('https://jsonplaceholder.typicode.com/posts?_start=0&_limit=5').then((response) => {
        this.posts = response.data;
        this.loading = false;
        console.log(response.data)
      })
    }
  }
</script>

<style>
  #posts{
    padding: 50px 0;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: space-around;
    flex-wrap: wrap;
  }

  .post_loading{}

  .post_loading p{}

  .post_loading .spin{
    width: 100px;
    height: 100px;
    border-top: 1px #000 solid;
    border-radius: 50%;
    display: block;
    margin: auto;
    animation: spin .8s linear infinite;
  }

  .post_item{
    width: 370px;
    margin-bottom: 20px;
  }

  .post_item img{
    max-width: 500px;
    width: 100%!important;
  }
  
  .post_item p{
    margin: 10px 0;
    padding: 0;
    text-align: left;
  }

  .item_title{
    font-size: 20px;
    color: #000;
  }

  .item_body{}

  
  @keyframes spin{
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
</style>