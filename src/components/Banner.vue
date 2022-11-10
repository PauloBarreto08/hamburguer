<template>
    <div id="main-banner">
      <h1 class="text-7xl text-center text-white bg-stone-900 p-4 pr-10 italic">Make Your Burger</h1>
    </div>
  </template>
  
  <script>
  
  export default {
      name: 'Banner',
  
  }
  </script>
  
  <style scoped>
      #main-banner {
        background-image: url('../assets/burger.jpg');
        background-position: 0 -350px;
        background-size: cover;
        height: 680px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }
  </style>