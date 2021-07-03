<template>
  <div>
    <h1>Vue Posts</h1>

    <div class="posts-wrapper">
      <blog-post 
        v-for="post in posts" 
        v-bind:post="post" 
        v-bind:key="post.id" 
        v-bind:headingSize="headingFontSize" 
        v-bind:descriptionSize="descriptionFontSize"
        v-on:increaseFont="headingFontSize += 0.1"
        v-on:decreaseFont="onDecreaseFontSize"
      />
    </div>
  </div>
</template>

<script>
import BlogPost from './components/BlogPost.vue';
import axios from 'axios';

export default {
  components: {BlogPost},
  data(){
    return {
      posts: [],
      headingFontSize: 1,
    };
  },
  computed:{
    descriptionFontSize(){
      return this.headingFontSize / 100 * 80;
    }
  },
  mounted(){
    this.fetchPosts();
  },
  methods: {
    fetchPosts(){
      axios.get('https://jsonplaceholder.typicode.com/posts')
        .then((response) =>{
          this.posts = response.data;
        })
        .catch((error) => {
          console.log('API Failded to load',error);
        });
    },
    onDecreaseFontSize(decreaseAmount){
      this.headingFontSize -= decreaseAmount;
    }
  },
}
</script>