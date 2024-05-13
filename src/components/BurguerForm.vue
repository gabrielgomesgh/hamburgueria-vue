<script>
export default{
    Name: "BurguerForm",
    data(){
        return{
            breads: null,
            meats: null,
            opcionaisdata: null,
            name: null,
            bread: null,
            meat: null,
            opcionais: [],
            status: "solicitado",
            msg: null
        }
    },
    methods:{
        async getIngredients(){
            const req = await fetch("http://localhost:3000/ingredientes")
            const data = await req.json();
            this.meats = await data.carnes;
            this.opcionaisdata = await data.opcionais;
            this.breads = await data.paes;
        },
        async createBurguer(e){
            e.preventDefault();
            
            const data = {
                nome: this.name,
                carnes: this.meat,
                opcionais: Array.from(this.opcionais),
                paes: this.bread,
                status: "Solicitado"
            }
            // console.log(data);
            const dataJson = JSON.stringify(data);

            // POST METHOD
            const req = await fetch("http://localhost:3000/burgers", {
                method: 'POST',
                headers: {"Content-Type": "application/json"},
                body: dataJson
            })
            
            this.name = '';
            this.meat = '';
            this.opcionais = '';
            this.bread = '';

        }
    },
    mounted(){
        this.getIngredients();
    }
}
</script>

<template>
    <section id="pedidoForm">
        <h1>Campo de pedido:</h1>
        <form id="burguer-form" @submit="createBurguer">
            <div class="input-container">
                <label for="name">Nome</label>
                <input type="text" name="name" id="nome" v-model="name">
            </div>

            <div class="input-container">
                <label for="bread">Pão</label>
                <select type="text" name="bread" id="bread" v-model="bread">
                    <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
                </select>
            </div>

            <div class="input-container">
                <label for="meat">Carne</label>
                <select type="text" name="meat" id="meat" v-model="meat">
                    <option v-for="meat in meats" :key="meat.id" :value="meat.tipo">{{ meat.tipo }}</option>
                </select>
            </div>

            <div class="input-container">
                <label for="opcionais">Selecione os opcionais</label>
                <div class="checkbox-container checkbox-container-submit" v-for="opcional in opcionaisdata" :key="opcional.id" :value="opcional.tipo">
                    <input class="checkbox" type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                    <span class="span-checkbox">{{ opcional.tipo }}</span>
                </div>
            </div>

            <div class="input-container submit">
                <input class="submit" type="submit" value="Criar meu hambúrguer!">
            </div>

        </form>
    </section>
</template>

<style scoped>
section{
    background-color: #181818;
    padding: 30px;
}
h1{
    text-align: center;
    color: white;
    font-size: 1.8rem;
    font-weight: 500;
}
label{
    color: #EFA335;
    display: block;
    font-size: 1.2rem;
    font-weight: 500;
}
#burguer-form{
    display: flex;
    justify-content: center;
    margin-left: auto;
    margin-right: auto;
    flex-wrap: wrap;
    max-width: 80vw;
}
.input-container{
    width: 100%;
    margin: 10px;
}
@media (min-width: 1000px) {
    .input-container{
        width: 35vw;
        margin: 10px;
    }
    section{
        padding: 80px;
    }
}
input, select{
    width: 100%;
    height: 2.5rem;
    font-size: 1rem;
    border: 0;
    border-radius: 4px;
    padding: 6px;
}
input.checkbox{
    height: 100%;
    width: 25px;
}
div.submit{
    width: 72vw;
}
input.submit{
    height: 3rem;
    background-color: #EFA335;
    font-size: 1.1rem;
    font-weight: 500;
}
input.submit:hover{
    color: #EFA335;
    background-color: #181818;
    border: 2px solid #EFA335;
}
.checkbox-container-submit{
    display: inline-table;
}
.span-checkbox{
    color: white;
    font-size: 1.2rem;
}
</style>