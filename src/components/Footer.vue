<template>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
    <footer>
    <ul class="social_icon">
        <li><a href="https://github.com/JuuhSouza"><i class="fa-brands fa-github"></i></a></li>
        <li><a href="https://www.linkedin.com/in/j%C3%BAlia-souza-0577572b2/"><i class="fa-brands fa-linkedin"></i></a></li>
    </ul>
    <ul class="menu">
        <li><router-link to="/" @click="closeMenu"> Inicio </router-link></li>
        <li><router-link to="/pedidos" @click="closeMenu"> Dashboard </router-link></li>
    </ul>

    <p>Júlia Souza | &copy; 2026 Make Your Burger</p>
    
   </footer>
</template>

<script>
    export default{
        name : 'Footer'
    }
</script>

<style>
footer {
    position: relative;
    widows: 100%;
    background: var(--nav-background-color);
    min-height: 100px;
    padding: 20px 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: -3em;
}

footer .social_icon,
footer .menu {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px 0;
}

footer .social_icon li,
footer .menu{
    list-style: none;
}

footer .social_icon li a {
    font-size: 2em;
    color: #fff;
    margin: 0 10px;
    display: inline-block;
    transition: 0.5s;
}

footer .social_icon li a:hover {
    transform: translateY(-10px);
}

footer .menu li a{
    font-size: 1.2em;
    color: var(--color-text);
    margin: 0 10px;
    text-decoration: none;
    opacity: 0.75;
    transition: .5s ease;
}

footer .menu li a:hover {
    opacity: .6;
}

footer .menu li .router-link-active {
    color: #fcba03 !important;
    font-weight: bold;
    opacity: 1;
}
footer p {
    color: white;
    text-align: center;
    margin-top: 15px;
    margin-bottom: 10px;
    font-size: 1em;
}

</style>