<template>
  <div class="main-container p-[39px]">
   <h1 class="flex justify-center text-5xl m-10 font-bold">Pedidos</h1>
   <Dashboard/>
 </div>
</template>

<script>
import Dashboard from '@/components/Dashboard.vue'

export default {
name: 'Pedidos',
components: {
 Dashboard

}
}
</script>

<style scoped>

</style>