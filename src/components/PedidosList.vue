<script>
export default{
    name: "PedidosList",
    data(){
        return{
            pedidos: null,
            status: null,
            newStatusValue: ''
        }
    },
    methods:{
        async getPedidos(){
            const req = await fetch('http://localhost:3000/burgers');
            const data = await req.json();
            this.pedidos = await data;
            console.log(data);
        },
        async deletePedido(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'DELETE',
                headers: { "Content-Type": "application/json"},
            })
        },
        async getStatus(){
            const req = await fetch('http://localhost:3000/status')
            const data = await req.json();
            this.status = await data;
            console.log(this.status);
            console.log(this.status[0].tipo);
        },
        async changeStatus(newStatus, id){
            const dataJson = {
                status: newStatus
            }
            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                methods: 'POST',
                headers: {"Content-Type": "application/json"},
                body: dataJson
            })
        },
        mudou(newStatus, id){
            console.log(`NEW STATUS: ${newStatusValue}. ID: ${id}`)
        }
    },
    mounted(){
        this.getPedidos();
        this.getStatus();
    }
}
</script>

<template>
    <div id="pedidos-list">
        <h1>Lista de Pedidos</h1>
        <div v-for="pedido in pedidos" :key="pedido.id" class="pedido">
            Cliente: {{ pedido.nome }},
            Pão: {{ pedido.paes }},
            Carne: {{ pedido.carnes }},
            Opcionais: {{ pedido.opcionais }},
            Status: {{ pedido.status }}.
            <select name="status" id="status" v-model="newStatusValue" @change="mudou(this.status.tipo, pedido.id)" >
                <option v-for="statusPedido in status" :key="statusPedido.id" :value="statusPedido.tipo">{{ statusPedido.tipo }}</option>
            </select>
            <button @click="deletePedido(pedido.id)">Excluir Pedido</button>
        </div>
    </div>
</template>

<style scoped>
h1{
    text-align: center;
}
</style>