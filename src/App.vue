<script setup>
    import Header from './components/Header.vue'
    import Quotes from './components/Quotes.vue';
    import Background from './components/Background.vue';
</script>

<template>
    <Background></Background>
    <Header></Header>
    <Quotes></Quotes>
</template>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500;700&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Comfortaa:wght@300;400;500;700&;&display=swap');

    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }


    html, body {
        height: 100%;
    }
    body{
    background-color: #F1F6F9;
    }
</style>
