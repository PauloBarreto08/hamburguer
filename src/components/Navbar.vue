<template>
  <div id="nav">
    <div class="grid grid-cols-6 gap-4 bg-stone-900"> 
      <div class="w-10 col-start-1 ml-11 mt-4 mb-5">
        <router-link to="/" id="logo-url">
          <img :src="logo" :alt="alt" id="logo" >
        </router-link>
      </div>
      <div class="col-end-8 text-amber-500 mr-20 mt-6">  
        <router-link class="m-6" to="/">Home</router-link> 
      <router-link to="/pedidos">Pedidos</router-link>  
    </div>
</div>
</div>
</template>

<script>
export default {
name: 'Navbar',
props: ["logo", "alt"]
}
</script>

<style scoped>
#nav a {
color: #FCBA03;
text-decoration: none;
transition: .5s;
}
</style>
