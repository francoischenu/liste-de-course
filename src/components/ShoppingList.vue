<template>
  <h1>Liste de course</h1>
  <ul>
    <li v-for="ingredient in newIngredients" :key=ingredient>
      {{ ingredient.name }} {{ ingredient.quantity }}
    </li>
  </ul>
</template>
<script>
import { recipe1, recipe2, recipe3 } from '../assets/recipes'

export default({
  setup() {
    const recipes = [ recipe1, recipe2, recipe3 ];

    const rawIngredients = [];
    recipes.forEach(({ ingredients }) => {
      rawIngredients.push(ingredients);
    });
    const ingredients = rawIngredients.flat();

    const newIngredients = [];
    ingredients.forEach((ingredient) => {
      const duplicate = newIngredients.find((newIngredient) => newIngredient.name === ingredient.name);

      if (!duplicate) {
        newIngredients.push(ingredient);
      } else {
        const index = newIngredients.findIndex(({ name }) => name === ingredient.name);
        const newQuantity = Number.parseFloat(newIngredients[index].quantity) + Number.parseFloat(ingredient.quantity);
        newIngredients.splice(index, 1, {...ingredient, quantity: newQuantity});
      }
    })

    return {
      ingredients,
      newIngredients,
    }
  },
})
</script>