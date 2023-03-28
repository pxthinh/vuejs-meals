<template>
     <header class="bg-white showdow-md h-16 flex justify-between items-stretch">
      <router-link :to="{ name: 'home' }" class="inline-flex items-center h-full px-5">
        Home
      </router-link>
      <div class="flex items-center gap-1">
        <router-link :to="{name: 'byName' }" class="inline-flex px-2 h-full transition hover:bg-purple-200">Search meal</router-link>
        <router-link :to="{name: 'byLetter' }" class="inline-flex px-2 h-full transition hover:bg-purple-200">Meals By Letter</router-link>
        <router-link :to="{name: 'ingredients' }" class="inline-flex px-2 h-full transition hover:bg-purple-200">Meals by Ingredients</router-link>
      </div>
    </header>
</template>