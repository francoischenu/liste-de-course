<template>
  <h1>Liste de course</h1>
  <div class="row">
    <div class="col-lg-4 col-s-12" v-for="category in categories" :key="category">
      <div class="category-card">
        <h2>{{ category[0].category }}</h2>
        <div v-for="ingredient in category" :key=ingredient class="ingredient-row">
          <div class="ingredient-name">{{ ingredient.name }}</div>
          <div class="ingredient-quantity">{{ ingredient.quantity }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { recipe2, recipe3, recipe4, recipe5, recipe6, recipe7, recipe8 } from '../assets/recipes'

export default({
  setup() {
    const recipes = [ recipe2, recipe3, recipe4, recipe5, recipe6, recipe7, recipe8 ];

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
    });

    const vegetables = newIngredients.filter(({ category }) => category === "légumes");
    const fresh = newIngredients.filter(({ category }) => category === "frais");
    const dry = newIngredients.filter(({ category }) => category === "épicerie");

    const categories = [vegetables, fresh, dry];

    return {
      categories,
      newIngredients,
    }
  },
})
</script>

<style scoped>
h1, h2, div {
  text-align: center;
}

h1, h2 {
  margin-bottom: 2rem;
}

.category-card {
  border: #1f001f solid 1px;
  margin: 2rem;
  padding: 2rem 0;
}

.ingredient-row {
  margin: 0 4rem;
  display: flex;
  justify-content: space-between;
}

.ingredient-name, .ingredient-quantity {
  display: flex;
}
</style>