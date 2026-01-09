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
       box-shadow: 2px 2px 2px var(--background-color-men);
       border-radius: 5px;
       padding: 10px;
       max-width: 400px;
       margin: 20px auto;
       margin-top:-.5em ;
    }
</style>