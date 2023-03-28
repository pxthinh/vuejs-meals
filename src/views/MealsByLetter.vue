<template>
       <div class="flex justify-center gap-2 mt-2">
        <router-link :to="{name: 'byLetter', params:{letter}}" v-for="letter of letters">
            {{ letter }}
        </router-link>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-5">
       <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal"/>
    </div>
</template>

<script setup>
import { computed } from "@vue/reactivity"
import { onMounted, watch } from "vue"
import { useRoute } from "vue-router";
import store from '../store';
import MealItem from '../components/MealItem.vue';

const route = useRoute();
const letters = "ABCDEFGHIKLMNOPQRSTUVWXYZ".split('');
const meals = computed(() => store.state.mealsByLetter)

watch(route, () => {
    store.dispatch('searchMealByLetters', route.params.letter)
})

onMounted(() => {
    store.dispatch('searchMealByLetters', route.params.letter)
})
</script>