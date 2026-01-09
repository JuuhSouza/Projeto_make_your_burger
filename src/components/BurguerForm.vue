<template>
    <div class="card-container-name">
            <form id="burger-form" @submit="createBurger">
                <div class="card-step">
                    <div class="card-header">
                        <!-- <span class="step-number"> 01 </span> -->
                         <label for="nome"> Nome do cliente: </label>
                    </div>
                         <div class="input-field">
                             <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome" required>
                        
                        </div>
            </div>
    
            <!-- PÃES -->
                <div class="card-step">
                    <div class="card-header">
                       <!--  <span class="step-number"> 02 </span> -->
                         <label for="pao"> Escolha o pão : </label>
                         <div class="input-field">
                              <select name="pao" id="pao" v-model="pao" required>
                            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo"> {{pao.tipo}}</option>
                            </select>
                         </div>
                    </div>
                </div>
                <!-- CARNES -->
                <div class="card-step">
                    <div class="card-header">
                        <!-- <span class="step-number"> 03 </span> -->
                            <label for="carne"> Escolha a carne : </label>
                         <div class="input-field">
                              <select name="carne" id="carne" v-model="carne" required>
                             <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo"> {{carne.tipo}}</option>
                            </select>
                         </div>
                    </div>
                </div>

                 <!-- OPCIONAIS -->
                <div class="card-step">
                    <div class="card-header">
                       <!--  <span class="step-number"> 04 </span> -->
                             <label id="opcionais-title" for="opcionais"> Escolha os complementos : </label>
                        
                    <div id="opcionais-container" class="input-container">
                        <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id" >
                            <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                            <span>{{opcional.tipo}}</span>
                        </div>
                    </div>
                </div>
                </div>
                    <div class="input-container">
                        <input type="submit" class="submit-btn" value="Criar meu burger!">

                    </div>
                    <Message :msg="msg" v-show="msg"/>
                </form>
    </div>
    
</template>

<script>
    import Message from './Message.vue';

    export default{
        name: 'BurguerForm',
        data(){
            return{
                paes: null,
                carnes: null,
                opcionaisdata: null,
                nome: null,
                pao: null,
                carne: null,
                opcionais: [],

                msg: null
            }
        },
        methods:{
            async getIngredientes(){
                /* API */
                const req = await fetch('http://localhost:3001/ingredientes');
                const data = await req.json();

                this.paes = data.paes;
                this.carnes = data.carnes;
                this.opcionaisdata = data.opcionais;
            },
            async createBurger(e){
                e.preventDefault();
                
                const data ={
                    nome: this.nome,
                    pao: this.pao,
                    carne: this.carne,
                    opcionais: Array.from(this.opcionais), /* objeto array */
                    status: "solicitado"
                }

                const datajson = JSON.stringify(data); /* transformar em texto */

                /* REQUIsICÃO PARA O JSON E CADASTRAR O PEDIDO*/
                const req = await fetch('http://localhost:3001/burgers',{
                   method: 'POST',
                   headers: { "content-Type": "application/json" },
                   body: datajson
                });
                const res = await req.json();

                /*  colocar mensagem no sistema */
                this.msg = `Pedido N° ${res.id} criado com sucesso`

                /* limpar msg */
                setTimeout(() => this.msg = "", 3000)

                /* limpar campos */
                this.nome = "";
                this.carne = "";
                this.pao = "";
                this.opcionais = [];
            }
        },
        mounted(){
            this.getIngredientes();
        },
        components: {
            Message
        }
    }
</script>

<style acoped> 
    .card-container-name{
    padding: 40px 20px;
    display: flex;
    margin-top:-2em ;
    }

    #burger-form {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 25px;
    }

    .card-step{
    flex: 1 1 280px;
    min-height: 250px;
    border: 2px solid var(--border-left);
    border-radius: 20px;
    padding: 30px;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    transition: all .5s ease;
    }

    .input-container:last-child {
        grid-column: 1 / -1; 
        display: flex;
        justify-content: center;
    }
    .card-step:hover{
        transform: translateY(-5px);
    }

    .card-step:last-of-type {
    flex: 2 1 500px;
    max-width: 620px;
}

/*     .step-number{
        background-color:green ;
        color: #000;
        width: 35px;
        height: 35px;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
        margin-right: 15px;
    } */

    .card-header label{
        font-size: 1.2rem;
        color: black;
        border:none;
        padding: 0;
    }

    .card-header::before {
        content: "";
        display: block;
        width: 5em;
        height: 5em;
        margin: 0 auto 15px;
        background-size: contain;
        background-repeat: no-repeat;
        background-position: center;
    }

.card-step:nth-child(1) .card-header::before {
    background-image: url('https://cdn-icons-png.flaticon.com/512/1077/1077114.png'); 
}
.card-step:nth-child(2) .card-header::before {
    background-image: url('https://img.freepik.com/vetores-premium/hamburguer-de-25-ingredientes-parte-3_760677-198.jpg?semt=ais_hybrid&w=740&q=80');
}
.card-step:nth-child(3) .card-header::before {
    background-image: url('https://cdn-icons-png.flaticon.com/512/4853/4853335.png');
}
.card-step:nth-child(4) .card-header::before {
    background-image: url('https://static.vecteezy.com/ti/vetor-gratis/p1/5895632-hamburguer-soda-bebida-e-donut-cartoon-icone-ilustracao-alimento-objeto-icone-conceito-isolado-premium-plano-cartoon-estilo-vetor.jpg');
    width: 10em;
    height: 10em;
    flex-shrink: 0; 
    margin-bottom: -22px;
    margin-top:-1em 
}

.card-header {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    width: 100%;
}

    .input-container {
        width: 100%;
        display: flex;
        justify-content: center;
        margin-top: -12px;
    }

    input, select {
        width: 100%;
        padding: 10px 20px;
        margin: 10px;
        border: 2px solid #eee;
        border-radius: 8px;
        font-size: 1rem;
        outline: none;
    }

    #opcionais-container{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); 
    gap: 10px;
    width: 100%;
    padding: 15px;
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 12px;
    }

    #opcionais-title{
        width: 100%;
        margin-bottom: 20px;
    }

    .checkbox-container{
        display: flex;
        align-items: center;
        margin-bottom:20px ;
        cursor: pointer;
        padding: 10px;
        border-radius: 8px;
    }

    .checkbox-container input{
        width: 20px;
        height: 20px;
        cursor: pointer;
        accent-color: #fcba03;
    }

    .checkbox-container span{
        margin-left:10px;
        color: var(--input-color);
        font-size: 14px;
        font-weight: bold;
    }

    .submit-btn{
        width: fit-content;
        background-color: var(---background-btn-form);
        color: white;
        font-weight: bold;
        font-family: var(--font);
        border: 2px solid #222;
        padding: 18px;
        cursor: pointer;
        transition: all .5s ease;
        border-radius: 20px 5%;
        text-transform: uppercase;
        font-size: 20px;
        margin-top: -1px;
        box-shadow: 0 5px 15px rgba(0,0,0,0.2);
    }

    .submit-btn:hover{
    background-color: var(--border-left);
    color: #222;
    border-color: var(--border-left);
    transform: translateY(-3px);
    }

    .submit-btn:active {
    transform: translateY(-1px);
}

</style>