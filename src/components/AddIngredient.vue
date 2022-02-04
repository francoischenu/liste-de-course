<template>
  <section class="container">
    <form @submit.prevent="addIngredient">
      <div>
        <label for="ingredienttext">Ingrédient</label>
        <input type="text" id="ingredienttext" v-model="enteredName" />
      </div>
      <div>
        <label for="ingredientQuantity">Quantitée</label>
        <input id="ingredientQuantity" v-model="enteredQuantity" />
      </div>
      <div>
        <label for="ingredientCategory">Catégorie</label>
        <select id="ingredientCategory" v-model="enteredCategory" class="form-select" aria-label="Default select example">
          <option value="légumes">Fruits et légumes</option>
          <option value="frais">Viande et produits frais</option>
          <option value="épicerie">Epicerie</option>
        </select>
      </div>
      <p v-if="invalidInput">Please enter a valid ingredient text (non-empty).</p>
      <button>Add Ingredient</button>
    </form>
  </section>
</template>

<script>
import { ref, watch } from "vue";

export default {
  emits: ["add-ingredient"],
  setup(_, context) {
    const enteredName = ref("");
    const enteredQuantity = ref("");
    const enteredCategory = ref("");
    const invalidInput = ref(false);

    watch(invalidInput, function (val) {
      if (val) {
        console.log("Analytics: Invalid Input");
      }
    });

    function addIngredient() {
      invalidInput.value = false;
      if (enteredName.value === "" || enteredQuantity.value === "") {
        invalidInput.value = true;
        return;
      }
      const name = enteredName.value;
      const quantity = enteredQuantity.value;
      const category = enteredCategory.value;
      context.emit("add-ingredient", { name, quantity, category });
      enteredName.value = "";
      enteredQuantity.value = "";
      enteredCategory.value = "";
    }

    return {
      enteredName,
      enteredQuantity,
      enteredCategory,
      invalidInput,
      addIngredient,
    };
  },
};
</script>

<style scoped>
form {
  text-align: center;
}

label {
  display: block;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

input {
  font: inherit;
  display: block;
  width: 100%;
  margin-bottom: 0.5rem;
}
</style>