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
      logoEndereco: '../public/img/logo.png'
    }
  }
}
</script>

<template>
  <header>
    <Navbar :logoSrc="logoEndereco" />
  </header>

  <RouterView />

  <Footer />
</template>

<style scoped>
  
</style>