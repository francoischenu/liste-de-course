<template>
  <div>
    <ingredients-list :ingredients="filteredIngredients"></ingredients-list>
    <add-ingredient @add-ingredient="addIngredient"></add-ingredient>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

import IngredientsList from "./IngredientsList.vue";
import AddIngredient from "./AddIngredient.vue";

export default {
  components: {
    IngredientsList,
    AddIngredient,
  },
  setup() {
    const ingredients = ref([]);

    const filteredIngredients = computed(function() {
      return ingredients.value.filter(
        (ingredient) => !ingredient.name.includes("Angular") && !ingredient.name.includes("React")
      );
    });

    function addIngredient(res) {
      console.log(res);
      const { name, quantity } = res;
      const newIngredient = {
        id: new Date().toISOString(),
        name,
        quantity,
      };
      ingredients.value.push(newIngredient);
    }

    return {
      filteredIngredients: filteredIngredients,
      addIngredient: addIngredient
    };
  }
};
</script>