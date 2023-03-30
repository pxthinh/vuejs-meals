<template>
     <div class="bg-white shadow rounded-x1">
            <router-link :to="{name: 'mealDetails', params: {id: meal.idMeal}}">
                <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl w-full h-48 object-cover" />
            </router-link>
            <div class="p-3">
            <h3 class="p-3 font-bold">{{ meal.strMeal }}</h3>
            <p class="mb-4">
                {{ $filters.truncateWords(meal.strInstructions, 20) }}
            </p>
            <div class="p-3 flex items-center justify-between">
              <YoutubeButton :href="meal.strYoutube">Youtube</YoutubeButton>
                <router-link to="/" class="px-3 py-2 rounded border-2 border-purple-600 hover:bg-purple-500 hover:text-white transition-colors">
                    View
                </router-link>
            </div>
            </div>
        </div>
</template>

<script setup>
import YoutubeButton from '../components/YoutubeButton.vue';

const { meal } = defineProps({
    meal: {
        required: true,
        type: Object
    }
})
</script>