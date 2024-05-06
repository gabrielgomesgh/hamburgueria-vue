<script>
export default{
    name: "Navbar",
    props: ['imgEndereco']

}
</script>

<template>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">
            <img :src="imgEndereco" alt="logo" id="logo">
        </RouterLink>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/pedidos">Pedidos</RouterLink>
      </nav>
    </div>
</template>