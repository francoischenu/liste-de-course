<template>
  <div>
    <MainMenu @switch-page="onSwitchPage"/>
    <MyRecipes v-if="currentPage === 'recipes'"/>
    <CourseIngredients v-else-if="currentPage === 'ingredients'"/>
    <ShoppingList v-else-if="currentPage === 'shoppingList'"/>
  </div>
</template>

<script>
import { ref } from 'vue';

import CourseIngredients from './components/CourseIngredients.vue';
import MyRecipes from './components/MyRecipes.vue';
import ShoppingList from './components/ShoppingList.vue';
import MainMenu from './components/MainMenu.vue';

export default ({
  components: {
    CourseIngredients,
    MyRecipes,
    ShoppingList,
    MainMenu,
  },
  setup() {
    const currentPage = ref('shoppingList');

    const onSwitchPage = (page) => {
      currentPage.value = page;
    };

    return {
      onSwitchPage,
      currentPage,
    };
  },
});
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
.container {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  max-width: 25rem;
  margin: 3rem auto;
  padding: 1rem;
  border-radius: 12px;
}
button {
  background-color: #1f001f;
  border: 1px solid #1f001f;
  border-radius: 0.125rem !important;
  color: white;
  font: inherit;
  cursor: pointer;
  padding: 0.5rem 1.5rem;
  margin-right: 1rem;
}
button:hover,
button:active {
  background-color: #ffffff;
  color: #1f001f;
}
</style>
