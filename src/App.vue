<template>

  <NavBar :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <Footer/>

</template>

<script>
  import NavBar from './components/NavBar.vue';
  import Footer from './components/Footer.vue';
  import logo from './assets/img/logo.png';

  export default {
    components: {
      NavBar, Footer
    },
    data(){
      return{
        logo_src: logo,
        app_name: "Make Your Burguer"
      }
    }
  }

</script>

<style>
  *{
    font-family: var(--font);
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container{
    margin: 50px;
    min-height:250px;
  }

h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: 222 ;
}
</style>