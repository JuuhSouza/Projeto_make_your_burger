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
       color:black;
       background-color: rgb(226, 226, 226);
       border: 2px solid black;
       border-radius: 5px;
       padding: 10px;
       max-width: 400px;
       margin: 30px auto;
    }
</style>