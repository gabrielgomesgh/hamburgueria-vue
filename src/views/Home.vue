<script>
  import Banner from '../components/Banner.vue'
  import BurguerForm from '../components/BurguerForm.vue'
  export default {
    name: "Home",
    components: {
      Banner,
      BurguerForm
    }
  }
</script>

<template>
  <main>
    <Banner />
    <BurguerForm />
  </main>
</template>
