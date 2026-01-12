<template>
  <Banner/>
  <div class="main-container"> 
    <Cards/>
    <h1>Monte seu hamburguer</h1>
    <BurguerForm/>
</div>
</template>

<script>
  import Banner from '../components/Banner.vue';
  import BurguerForm from '../components/BurguerForm.vue';
  import Cards from '../components/Cards.vue';
 
export default {
  name: "HomeView",
  components: {
    Banner, BurguerForm, Cards
  }
}
</script>

<style scoped>
  h1{
    font-family: var(--font);
    font-size: 2em;
    margin: 1em 10px;
    margin-top: 1em;
  }
</style>
