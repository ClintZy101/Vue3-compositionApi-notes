<template>
<div v-if="error">{{ error }}</div>
<div v-if="posts.length">
  <PostList  :posts="posts" />
</div>
<div v-else>Loading...</div>
<button @click="showPosts = !showPosts">Toggle Posts</button>
<button @click="posts.pop()">Delete a Post</button>
  
  <!-- <p>{{ ninjaOne.name }} - {{ ninjaOne.age }}</p>
  <p>{{ ninjaTwo.name }} - {{ ninjaTwo.age }}</p>
  <button @click="updateNinjaOne">Update NinjaOne</button>
  <button @click="updateNinjaTwo">Update NinjaTwo</button>

  <div style="marginTop: 3rem">
    <Computed />
  </div>  -->

 
</template>

<script>
import { reactive, ref } from "@vue/reactivity";
import Computed from '../components/Computed.vue';
import PostList from '../components/PostList.vue'

export default {
  name: "Home",
  components:{
    PostList,
    Computed
  },
  
  setup() {
    //  const p = ref(null)
    //  const name = ref('clint')
    //  const age = ref(29)
    //   const handleClick = () => {
    //     // console.log(p, p.value)
    //     // p.value.classList.add('test')
    //     // p.value.textContent = 'hello'
    //     // name = 'luigi'  {{this will not work}}
    //     name.value = 'luigi'
    //     age.value ='330'
    //   }

    const ninjaOne = ref({ name: "mario", age: 30 });
    const ninjaTwo = reactive({ name: "luigi", age: 31 });

    // You can't use primitive values (strings, boolean etc) in reactive
    // 

    const updateNinjaOne = () => {
      ninjaOne.value.age += 1;
    };

    const updateNinjaTwo = () => {
      ninjaTwo.age += 1;
    };

    const posts = ref([])

    const showPosts = ref(true)

    const error = ref(null)



    const load = async() => {
      try {
        let data = await fetch('http://localhost:3000/posts')
        if (!data.ok){
          throw Error('No data available')
        }
        posts.value = await data.json()
      }
      catch (err) {
        error.value = err.message
        console.log(error.value)
      }
    }

    load()

    return {
      ninjaOne,
      ninjaTwo,
      posts,
      updateNinjaOne,
      updateNinjaTwo,
      showPosts,
      error
    }
  },
 
};
</script>
