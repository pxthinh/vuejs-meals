<template>
    <div class="flex flex-col p-8">
        <div class="flex p-8 justify-center">
        <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search meal">
        </div>
    </div>
</template>

<script setup>
import { computed, onMounted } from 'vue'
import store from '../store';
import axiosClient from '../axiosClient.js';

const meals = computed(() => store.state.meals);


onMounted(async () => {
    const response = await axiosClient.get('list.php?i=list')
});
</script>