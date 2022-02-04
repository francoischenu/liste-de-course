<template>
  <button @click="onToggleIngredients">Show ingredients</button>
  <h1>{{ recipe.name }}</h1>
  <ul v-show="toggleIngredients">
    <li v-for="ingredient in recipe.ingredients" :key=ingredient>
      {{ ingredient.name }} {{ ingredient.quantity }}
    </li>
  </ul>
</template>

<script>
import {ref} from "@vue/reactivity";

export default({
  props: ["recipe"],
  setup() {
    let toggleIngredients = ref(false);

    const onToggleIngredients = (index) => {
      console.log(index)
      toggleIngredients.value = !toggleIngredients.value;
    }

    return {
      toggleIngredients,
      onToggleIngredients,
    }
  }
});
</script>