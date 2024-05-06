<script>
export default{
    name: "Navbar",
    props: ['logoSrc']

}
</script>

<template>
  <nav>
    <RouterLink to="/">
      <img :src="logoSrc" width="45px" alt="logo" id="logo">
    </RouterLink>

    <div class="links">
      <RouterLink class="link" to="/">Home</RouterLink>
      <RouterLink class="link" to="/pedidos">Pedidos</RouterLink>
    </div>
  </nav>
</template>

<style scoped>
  nav{
    padding: 0;
    display: flex;
    align-items: center;
    justify-content: space-around;
    background-color: #181818;
    padding-top: 11px;
    padding-bottom: 8px;
  }
  .links{
    display: flex;
  }
  .link{
    padding: 8px;
    font-size: 1.2rem;
  }
</style>