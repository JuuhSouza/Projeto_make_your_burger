<template>
    <nav id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>

        <button id="hamburger" @click="toggleMenu">
            <span></span>
            <span></span>
            <span></span>
        </button>

        <div id="nav-links" :class="{active: menuOpen}">
            <router-link to="/" @click="closeMenu"> Inicio </router-link> 
            <router-link to="/pedidos" @click="closeMenu"> Dashboard </router-link>
        </div>
    </nav>
</template>

<script>
    export default{
        name: "NavBar",
        props: ["logo", "alt"],
        data(){
            return{
                menuOpen : false
            }
        },
        methods:{
            toggleMenu(){
                this.menuOpen = !this.menuOpen
            },
            closeMenu(){
                this.menuOpen = false
            }
        }
    }
</script>

<style scoped>
    #nav{
        background-color: var(--nav-background-color);
        border-bottom: 1px solid #0D0D0D;
        padding: 15px 50px;
        display: flex;
        align-items: center;
        position: relative;
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
        color: var(--nav-color);
        text-decoration: none;
        margin: 12px;
        transition: all .4s ease;
        font-size: 1.2em;
    }

    #nav a:hover{
        color:var(--nav-color-hover);  
        transform: translateX(-2px);
    }

    #hamburger{
        border:none;
        cursor: pointer;
        display: flex;
        flex-direction: column;
        gap:3px;
    }

    #hamburger span{
        width: 25px;
        height: 3px;
        background: var(--nav-background-color
        );
        transition: .3s ease;
    }

    #nav-links{
        position: absolute;
        top: 50px;
        right: 0;
        background: var(--nav-background-color) ;
        width: 200px;
        display: none;
        flex-direction: column;
        box-shadow: 0 4px 10px rgba(0,0,0,.3);
        border-radius: 8px;
        z-index: 100;
    }

    #nav-links.active{
        display: flex;
    }

    #nav-links a{
        color:var(--nav-color);
        text-decoration: none;
        padding: 5px 20px;
        transition:.3s ease;
    }

    #nav-links a:hover{
        opacity: .7;
    }

</style>