<template>
    <Message :msg="msg" v-show="msg"/>
    <div id="burger-table">
        <div>
            <div id="burger-table-head">
                <div class="order-id"> #: </div>
                <div> Cliente: </div>
                <div> Pão: </div>
                <div>Carne: </div>
                <div>Opcionais: </div>
                <div>Ações: </div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
                <div class="order-number"> {{ burger.id }} </div>
                <div>{{ burger.nome }}</div>
                <div>{{ burger.pao }}</div>
                <div> {{ burger.carne }}</div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in burger.opcionais" :key="index"> {{ opcional }} </li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updateBurger($event, burger.id)">
                    <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo"> <!-- :selected faz com q todos os campos estejam com o status de solicitado ao iniciar-->
                        {{ s.tipo }}</option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)"> Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Message from './Message.vue';

    export default{
        name: "Dashboard",
        data(){
            return{
                burgers: null,
                burger_id: null,
                status: [],
                msg : null
            }
        },
        components: {
            Message
        },
        methods: {
            async getPedidos(){
                const req = await fetch("http://localhost:3001/burgers");
                const data = await req.json();
                
                this.burgers = data;

                console.log(this.burgers);
                /* RESGATAR STATUS */
                this.getStatus();
            },
            async getStatus(){
                const req = await fetch("http://localhost:3001/status");
                const data = await req.json();

                this.status = data;

            },
            async deleteBurger(id){
                const req = await fetch(`http://localhost:3001/burgers/${id}`,{
                    method : "DELETE"
                });
                const res = await req.json();
            
                /* MENSAGEMD E PEDIDO DELETADO */
                this.msg = `Pedido removido com sucesso!!`

                /* limpar msg */
                setTimeout(() => this.msg = "", 4000)


                this.getPedidos();
            },
            async updateBurger(event, id){
                const option = event.target.value; /* saber qual opção esta sendo selecionada */
                const dataJson = JSON.stringify({status: option}); /* atualizar no banco */
                const req = await fetch(`http://localhost:3001/burgers/${id}`,{
                    method: "PATCH",
                    headers: { "content-Type": "application/json" },
                    body: dataJson
                }); /* acessar no id da api e atualizar o status */
                const res = await req.json();

                /*  colocar mensagem no sistema */
                this.msg = `Pedido N° ${res.id} foi atualizado para ${res.status}`

                /* limpar msg */
                setTimeout(() => this.msg = "", 4000)

                console.log(res);

            }
        },
        mounted() {
            this.getPedidos();
        }
    }
</script>

<style scoped>
#burger-table{
    max-width: 1200px;
    margin: 0 auto;
} 

#burger-table-head,
#burger-table-rows,
.burger-table-row{
    display: flex;
    flex-wrap: wrap;
}

#burger-table-head{
    font-weight: bold;
    padding: 12px;
    border-bottom: 2px solid var(--border-dash);
}

#burger-table-head div,
.burger-table-row div{
    width: 19%;
}

.burger-table-row{
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid var(--border-form);
}

#burger-table-head .order-id,
.burger-table-row .order-number{
    width: 5%;
}

.burger-table-row div:last-child{
    display: flex;
    align-items: center;
    gap: 6px;
}

select{
    width: 9em;
}

.delete-btn{
    background-color: var(--background-delet);
    color: white;
    font-weight: bold;
    border: none;
    border-radius: 10px 5%;
    padding: 10px;
    font-size:16px;
    margin: 0 auto;
    cursor: pointer;
    transition: all .5s ease;
}

.delete-btn:hover{
    background-color: black;
}


</style>