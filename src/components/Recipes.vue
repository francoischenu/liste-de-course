<template>
    <div v-for="{ name, ingredients } in recipes" :key="name">
        <h1>{{ name }}</h1>
        <ul>
            <li v-for="ingredient in ingredients" :key=ingredient>
                {{ ingredient.text }} {{ ingredient.quantity }}
            </li>
        </ul>
    </div>
</template>
<script>
import { recipe1, recipe2 } from '../assets/recipes'

export default({
    setup() {
        const recipes = { recipe1, recipe2 };

        return {
            recipes,
        }
    },
})
</script>
