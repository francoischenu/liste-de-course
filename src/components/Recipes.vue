<template>
  <div v-for="recipe in recipes" :key="recipe">
    <SingleRecipe :recipe="recipe"/>
  </div>
</template>
<script>
import { recipe2, recipe3 } from '../assets/recipes';

import SingleRecipe from "./SingleRecipe.vue";

export default({
  components: { SingleRecipe },
  setup() {
    const recipes = { recipe2, recipe3 };

    return {
      recipes,
    }
  },
})
</script>

<style scoped>
div {
  text-align: center;
}
</style>