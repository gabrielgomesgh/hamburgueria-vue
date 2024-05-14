<script>
export default{
    name: "PedidosList",
    data(){
        return{
            pedidos: null,
            status: null,
            numeracao: 1
        }
    },
    methods:{
        async getPedidos(){
            const req = await fetch('http://localhost:3000/burgers');
            const data = await req.json();
            this.pedidos = await data;
        },
        async deletePedido(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'DELETE',
                headers: { "Content-Type": "application/json"},
            })
            this.getPedidos();
        },
        async getStatus(){
            const req = await fetch('http://localhost:3000/status')
            const data = await req.json();
            this.status = await data;
        },
        async changeStatus(newStatusValue, id){
            const data = {
                status: newStatusValue
            }
            const dataJson = JSON.stringify(data);
            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: 'PATCH',
                headers: {"Content-Type": "application/json"},
                body: dataJson
            })
        }
    },
    mounted(){
        this.getPedidos();
        this.getStatus();
    }
}
</script>

<template>
    <div id="pedidos-list" >
        <h1>Lista de Pedidos</h1>
        <div id="pedidos" class="pedido">
            
            <!-- Cliente: {{ pedido.nome }},
            Pão: {{ pedido.paes }},
            Carne: {{ pedido.carnes }},
            Opcionais: {{ pedido.opcionais }},
            Status: {{ pedido.status }}.

            <select name="status" id="status" v-model="pedido.status" @change="changeStatus(pedido.status,pedido.id)" >
                <option v-for="statusPedido in status" :key="statusPedido.id" :value="statusPedido.tipo">
                    {{ statusPedido.tipo }}
                </option>
            </select>

            <button @click="deletePedido(pedido.id)">Excluir Pedido</button> -->


            <table>
                <tr class="titles-table">
                    <th>#</th>
                    <th>Nome</th>
                    <th class="responsive">Pão</th>
                    <th class="responsive">Carne</th>
                    <th class="responsive">Opcionais</th>
                    <th>Status</th>
                    <th>Ação</th>
                </tr>
                <tr id="pedidos" v-for="pedido in pedidos" :key="pedido.id">
                    <td>  </td>
                    <td> {{ pedido.nome }} </td>
                    <td class="responsive"> {{ pedido.paes }} </td>
                    <td class="responsive"> {{ pedido.carnes }} </td>
                    <td class="responsive">
                        <ul v-for="opcionais in pedido.opcionais">
                            <li> {{ opcionais }} </li>
                        </ul>
                    </td>
    
                    <td> 
                        <select name="status" id="status" v-model="pedido.status" @change="changeStatus(pedido.status, pedido.id)">
                            <option v-for="statusPedido in status" :key="statusPedido.id" :value="statusPedido.tipo"> {{ statusPedido.tipo }}</option>
                        </select>
                    </td>
    
                    <td>
                        <button @click="deletePedido(pedido.id)">Excluir pedido</button>
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<style scoped>
h1{
    text-align: center;
    font-size: 2rem;
    padding: 50px;
    font-weight: 500;
}
h2{
    text-align: center;
    margin-top: 10vh;
}
table,th,tr, td{
    border-bottom: 1px solid black;
    border-collapse: collapse;
}
th,td{
    padding: 10px;
}
table{
    margin-left: auto;
    margin-right: auto;
}
th{
    font-weight: bold;
}
.titles-table{
    border-bottom: 2px solid black;
}
button{
    background-color: #181818;
    color: #EFA335;
    border: 1px solid black;
    border-radius: 3px;
    padding: 10px;
    font-weight: 600;
}
select{
    padding: 9px;
}
@media (max-width: 770px) {
    .responsive{
        display: none;
    }
    #pedidos-list{
        height: 70vh;
    }
}
</style>