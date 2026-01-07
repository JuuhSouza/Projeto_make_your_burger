<template>
    <div id="main-banner">
        <h1>Burger banner</h1>
    </div>
    
</template>

<script>
    export default {
        name : 'Banner'
    }
</script>

<style scoped>
    :root{
        --banner-color: #ff0000;
    }

    #main-banner{
        background-image: url('../assets/img/burger.jpg');
        background-position: 0 -250px;
        background-size: cover;
        background-repeat: no-repeat;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }

    #main-banner h1{
        color: white;
        text-align: center;
        font-size:60px;
        background-color: rgb(60, 60, 60);
        padding: 20px 40px;
    }
</style>