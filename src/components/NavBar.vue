<template>
    <nav id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>

        <router-link to="/">Inicio</router-link> |
        <router-link to="/pedidos">Pedidos</router-link>
    </nav>
</template>

<script>
    export default{
        name: "NavBar",
        props: ["logo", "alt"]
    }
</script>

<style scoped>
    #nav{
        background-color: #333;
        border-bottom: 4px solid black;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    #nav #logo-url{
       margin: auto;
       margin-left: 0;
    }

    #logo{
        width: 40px;
        height: 40px;
    }

    #nav a{
        color: red;
        text-decoration: none;
        margin: 12px;
        transition: all .4s ease;
    }

    #nav a:hover{
        color: white;
    }



</style>