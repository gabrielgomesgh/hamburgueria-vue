<script>
import { RouterLink, RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

export default{
  components:{
    Navbar,
    Footer
  },
  data() {
    return{
      imgEndereco: '../public/img/logo.png'
    }
  }
}
</script>

<template>
  <header>
    <Navbar :src="imgEndereco" />
  </header>

  <RouterView />

  <Footer />

</template>

<style>

</style>