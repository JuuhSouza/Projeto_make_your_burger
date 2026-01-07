<template>
    <div> 
        <div>
            <div>
                <form id="burger-form" @submit="createBurger">
                    <div class="input-container">
                        <label for="nome"> Nome do cliente: </label>
                        <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
                    </div>
                    <!-- PÃES -->
                    <div class="input-container">
                        <label for="pao"> Escolha o pão : </label>
                            <select name="pao" id="pao" v-model="pao">
                            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo"> {{pao.tipo}}</option>
                            </select>
                    </div>
                    <!-- CARNES -->
                    <div class="input-container">
                        <label for="carne"> Escolha a carne : </label>
                            <select name="carne" id="carne" v-model="carne">
                             <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo"> {{carne.tipo}}</option>
                            </select>
                    </div>
                    <!-- OPCIONAIS -->
                    <div id="opcionais-container" class="input-container">
                        <label id="opcionais-title" for="opcionais"> Escolha os opcionais : </label>
                        <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id" >
                            <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                            <span>{{opcional.tipo}}</span>
                        </div>
                       
                    </div>
                    <div class="input-container">
                        <input type="submit" class="submit-btn" value="Criar meu burger!">
                        <Message :msg="msg" v-show="msg"/>
                    </div>
                </form>
            </div>
        </div>
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
                this.opcionais = "";
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
    #burger-form {
        max-width: 300px;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: bold;
        margin-bottom:15px;
        color:var(--title-form-color);
        padding: 15px 10px;
        font-family: var(--font);
        border-left: 4px solid var(--border-left);
    }

    input, select{
        padding: 10px 10px;
        width: 300px;
        font-size:var(--font-size-input);
        color:var(--input-color);
        font-family: var(--font);
        cursor:pointer;

    }

    #opcionais-container{
        flex-direction:row ;
        flex-wrap: wrap;
    }

    #opcionais-title{
        width: 100%;
    }

    .checkbox-container{
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom:20px ;
    }

    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span{
        margin-left:6px;
        font-weight: bold;
    }

    .submit-btn{
        background-color: var(---background-btn-form);
        color: white;
        font-weight: bold;
        font-family: var(--font);
        border: none;
        padding: 10px;
        cursor: pointer;
        transition: all .5s ease;
        border-radius: 20px 5%;
        font-size: 20px;
    }

    .submit-btn:hover{
        opacity: .5;
        transform: rotateY(-10deg);
    }

</style>