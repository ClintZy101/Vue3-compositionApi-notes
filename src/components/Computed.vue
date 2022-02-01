<template>
  <div class="computed">Computed</div>
  <input type="text" v-model="search" />
  <!-- <p>search term = {{ search }}</p> -->
  <div v-for="name in matchingNames" :key="name">{{ name }}</div>
  <div>
      <button @click="handleClick">Stop Watching</button>
  </div>
</template>

<script>
import { ref, computed, watch, watchEffect } from "vue";

export default {
  name: "Computed",

  setup() {
    const search = ref("");
    const names = ref([
      "mario",
      "yoshi",
      "luigi",
      "toad",
      "bowser",
      "koopa",
      "peach",
    ]);

    // watch(search, () => {
    //     console.log('watch function ran')
    // })

    // watchEffect(() => {
    //     console.log('watch effect ran', search.value)
    // })

    // to stop watching
    const stopWatch = watch(search, () => {
      console.log("watch function ran");
    });

    const stopEffect = watchEffect(() => {
      console.log("watch effect ran", search.value);
    });

    const handleClick = () => {
        stopWatch(),
        stopEffect()
    }

    const matchingNames = computed(() => {
      return names.value.filter((name) => name.includes(search.value));
    });
    return {
      names,
      search,
      matchingNames,
      handleClick
    };
  },
};
</script>

<style>
</style>