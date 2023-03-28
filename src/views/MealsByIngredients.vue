<template>
    <div class="p-8">
        <h1 class="text-4x1 font-bold mb-4">Ingredients</h1>
        <router-link :to="{ name: 'byIngredient', params: { ingredient: ingredient.idIngredient}}" v-for="ingredient of ingredients" :key="ingredient.id" 
        class="block bg-white rounded p-3 mb-3 shadow">
            <h3 class="text-2x1 font-bold">{{ ingredient.strIngredient }}</h3>
            <p>{{ ingredient.strDescription }}</p>
       </router-link>
    </div>
</template>

<script setup>
import { computed } from "@vue/reactivity"
import { onMounted } from 'vue';
import { useRoute } from "vue-router";
import store from '../store';

const route = useRoute();
const meals = computed(() => store.state.mealsByIngredient)

onMounted(() => {
    store.dispatch('searchMealByIngredients', route.params.ingredient)
})

</script>