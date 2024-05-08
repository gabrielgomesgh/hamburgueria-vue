<script>
    export default{
        name: "Banner",

    }
</script>

<template>
    <div class="main-container">
        <div>
            <h1>Monte seu hambúrguer</h1>
        </div>
        <div></div>
    </div>
</template>

<style scoped>
.main-container{
    height: 50vw;
    max-height: 500px;
    background-image: url('/public/img/burger.jpg');
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: space-around;
    color: white;
    font-size: 1.05rem;
}
h1{
    font-weight: 600;
}
</style>