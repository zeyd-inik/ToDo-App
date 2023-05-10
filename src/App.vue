<script setup>
import { RouterView } from 'vue-router';
import TheHeader from './components/UI/TheHeader.vue';
</script>
<template>
    <div class="app">
        <the-header></the-header>
        <RouterView></RouterView>
    </div>
</template>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,500;0,700;1,300&display=swap');
/* global styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Roboto', sans-serif;
}
</style>
