<template>
    <div class="flex flex-col p-8">
        <div class="flex p-8 justify-center">
        <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search meal">
    </div>

    <div class="flex justify-center gap-2 mt-2">
        <router-link :to="{name: 'byLetter', params:{letter}}" v-for="letter of letters">
            {{ letter }}
        </router-link>
    </div>
    </div>
</template>

<script setup>
import { computed, onMounted } from 'vue'
import store from '../store';
import axiosClient from '../axiosClient.js';

const meals = computed(() => store.state.meals);
const letters = "ABCDEFGHIKLMN".split('');

onMounted(async () => {
    const reponse = await axiosClient.get('/list.php?i=list')
    console.log(reponse.data);
});
</script>