<template>
  <Banner/>
    <div class="main-container">
      <h1 class="flex justify-center text-5xl m-10"><strong>Monte seu hamburguer</strong></h1>
      <BurgerForm/>
    </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import BurgerForm from '../components/BurgerForm.vue'

  export default {
    name: 'Home',
    components: {
      Banner,
      BurgerForm
    },
  }
</script>