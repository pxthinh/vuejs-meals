<template>
    <div class="p-8">
        <input type="text" v-model="keyword" class="rounded border-2 bg-white border-gray-200 w-full" placeholder="Search for ingredient"
            @change="search">
    </div>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
      <a href="#"
        @click.prevent="openIngredient(ingredient)"
        v-for="ingredient of computedIngredients"
        :key="ingredient.idIngredient"
        class="block bg-white rounded p-3 mb-3 shadow"
      >
        <h3 class="text-2xl font-bold mb-2">{{ ingredient.strIngredient }}</h3>
        <p>{{ $filters.truncateWords(ingredient.strDescription, 15) }}</p>
      </a>
    </div>
</template>

<script setup>
import { computed } from '@vue/reactivity'
import { onMounted, ref } from 'vue';
import axiosClient from '../axiosClient';
import { useRouter } from "vue-router";
import store from '../store';

const keyword = ref('');
const ingredients = ref([]);
const router = useRouter();

const computedIngredients = computed(() => {
    if(!computedIngredients) return ingredients;
    return ingredients.value.filter( (i) =>
            i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
    )
})

function openIngredient(ingredient) {
    console.log(ingredient);
  store.commit('setIngredient', ingredient)
  router.push({
    name: "byIngredient",
    params: { ingredient: ingredient.strIngredient },
  });
}

onMounted(() => {
    axiosClient.get('list.php?i=list')
    .then(({data}) => {
        ingredients.value = data.meals
    })
})
</script>