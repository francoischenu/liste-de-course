<template>
    <h1>Home</h1>
    <span>Add an ingredient</span>
    <form>
        <input v-model='ingredient'>
        <button @click='onAddIngredient(ingredient)'>Add ingredient</button>
    </form>
    {{ recipe }}
    {{ ingredients }}
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
    setup() {
        const ingredients = ref([]);
        const recipe = ref({
            name: '',
            ingredients,
        });

        const onAddIngredient = (ingredient) => {
            ingredients.value.push(ingredient);
        }

        return {
            recipe,
            ingredients,
            onAddIngredient,
        };
    },
    // props: {
    //     recipe: Object,
    // },
    // methods: {
    //     onAddIngredient: (ingredient) => {
    //         this.recipe.ingredients.push(ingredient);
    //     }
    // },
})
</script>
