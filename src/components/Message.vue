<template>
    <div class="mensage-container">
       <p> {{ msg }} </p>
    </div>
</template>

<script>
    export default{
        name: 'Message',
        props:{
            "msg" : String
        }
    }
</script>

<style scoped>
    .mensage-container{
       color:var(--color-men);
       background-color: var(--background-color-men);
       /* border: 2px solid var( --border-left); */
       border-radius: 5px;
       padding: 10px;
       max-width: 400px;
       margin: 30px auto;
    }
</style>