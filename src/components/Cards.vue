<template>
<div class="title-features">
    <h1>
        Serviços oferecidos
    </h1>
</div>


<div class="container">
    <div class="card-info">
        <div class="title">
            <img src="../assets/img/logo.png" alt="">
        </div>
        <div class="content">
            <p>Escolha cada detalhe do seu hambúrguer! Selecione o pão de sua preferência, o tipo de carne e todos os complementos opcionais para criar uma combinação única e do seu jeito.</p>
        </div>
    </div>

    <div class="card-info">
        <div class="title">
            <img src="../assets/img/pedidosIcone.png" alt="">
        </div>
        <div class="content">
            <p>Após realizar o pedido, ele é enviado diretamente para o nosso sistema. No dashboard, é possível acompanhar o progresso em tempo real, visualizar a fila de produção e atualizar o status de cada burger.</p>
        </div>
    </div>
</div>

</template>

<script>
    export default{
        name : 'Cards'
    }

</script>

<style scoped>
.title-features{
  margin: 1%;
}

.title-features h1 {
  font-size: 2.6em;
  font-family:var(--font);
  color: var(--title-color-card);
  text-align: center;
  margin: 2%;
  margin-top: 2em;
}

.container {
  display: flex;
  height: auto;
  min-height: 100vh 80px;
}

.card-info {
  padding: 2em;
  margin: 2em 2.5em;
  border: 2px solid var(--card-border);
  border-radius: 20px;
  transition: all .5s ease;
}

.card-info:hover {
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  transform: rotateY(-10deg);
  border: none;
}

.title h1 {
   font-family:var(--font);
  color: var(--title-color-card);
  margin: 12px;
  text-align: center;
  font-size: 2em;
}

.title img {
  margin: 12px;
  width: 20%;
  align-items: center;
  text-align: center;
  margin-left: 40%;
}

.content p {
  color: var(--p-color-card);
  font-size: 1em;
  text-align: center;
  font-family: var(--font-p);
}


</style>