<template>
    <div class="p-8">
        <input type="text" v-model="keyword" class="rounded border-2 border-gray-200 w-full" placeholder="Search for meals"
            @change="searchMeals">
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-5">
        <div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-x1">
            <router-link :to="{name: 'mealDetails', params: {id: meal.idMeal}}">
                <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl w-full h-48 object-cover" />
            </router-link>
            <div class="p-3">
            <h3 class="p-3 font-bold">{{ meal.strMeal }}</h3>
            <p class="mb-4">Lorem ipsum dolor sit amet consectetur adipisicing elit.</p>
            <div class="p-3 flex items-center justify-between">
                <a :href="meal.strYoutube" target="_blank"
                class="px-3 py-2 rounded border-2 border-red-600 bg-red-500 hover:bg-red-600 hover:text-white transition-colors"
                >Youtube</a>
                <router-link to="/" class="px-3 py-2 rounded border-2 border-purple-600 hover:bg-purple-500 hover:text-white transition-colors">
                    View
                </router-link>
            </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed } from '@vue/reactivity';
import { ref, onMounted } from 'vue';
import store from '../store';
import { useRoute } from 'vue-router';

const route = useRoute();
const keyword = ref('');
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
    store.dispatch("searchMeals", keyword.value);
}

onMounted(() => {
    keyword.value = route.params.name;
    if (keyword.value) {
        searchMeals()
    }
})
</script>