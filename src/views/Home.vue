<template>
<div v-if="showPosts">
<div v-if="error">{{ error }}</div>
  <div v-if="posts.length">
    <PostList :posts="posts" />
  </div>
  <div v-else>Loading...</div>
</div>
  
  <button @click="showPosts = !showPosts">Toggle Posts</button>
  <button @click="posts.pop()">Delete a Post</button>


</template>

<script>
import { ref } from '@vue/reactivity';
import Computed from "../components/Computed.vue";
import PostList from "../components/PostList.vue";
import getPosts from '../composables/getPosts'

export default {
  name: "Home",
  components: {
    PostList,
    Computed,
  },

  setup() {
    const {posts, error, load } = getPosts()
    load()

    const showPosts = ref(true)

    return {
      error,
      posts,
      showPosts
    };
  },
};
</script>
