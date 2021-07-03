<template>
  <div class="post">
    <img v-bind:src="postImage" alt="">
    <div class="post-content">
      <h2 v-bind:style="{fontSize: headingSize + 'em'}">{{ post.title }}</h2>
      <p v-bind:style="{fontSize: descriptionSize + 'em'}">{{ post.body }}</p>
      <button v-on:click="$emit('increaseFont')">Increase Font</button>
      <button v-on:click="$emit('decreaseFont',0.1)">Decrease Font</button>
    </div>
  </div>
</template>

<script>
export default {
  props : ['post','headingSize','descriptionSize'],
  data(){
    return {
      postImage: 'https://picsum.photos/400/250',
    };
  },
  created(){
    this.postImage += "?random="+this.post.id;
  },
}
</script>