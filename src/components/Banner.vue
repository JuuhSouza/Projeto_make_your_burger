<template>
    <div id="main-banner">
        <h1>Faça seu Hamburguer</h1>
    </div>
    
</template>

<script>
    export default {
        name : 'Banner'
    }
</script>

<style scoped>
    #main-banner{
        background-image: url('../assets/img/burger.jpg');
        background-position: 0 -190px;
        background-size: cover;
        background-repeat: no-repeat;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-banner h1{
        color: var(--color-p);
        text-align: center;
        font-size:3em;
        background-color: var(--background-color);
        padding: 20px 20px;
        border-radius: 20px 5%;
    }
</style>