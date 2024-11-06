<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <div class="w-full min-h-screen flex flex-col justify-center items-center bg-main">
    <h1 class="text-5xl">Hello</h1>
    <div class="flex flex-nowrap m-4 gap-2 items-center h-[45px] w-full justify-center ">
      <div class=" h-full bg-slate-300 rounded-xl w-[45rem]
       bg-secondary overflow-hidden shrink border border-stone-800 flex flex-nowrap items-center">
        <div class="h-[60%] flex items-center mx-3 opacity-65">
          <img class=" h-[80%] m-auto" src="./assets/search.svg">
        </div>
        <input type="text" placeholder="Masukkan sesuatu... " class="p-2 text-xl outline-none w-full bg-secondary">
        <div class="w-[2.5rem] h-[2rem] bg-orange mx-4 rounded-md">

        </div>
       

      </div>

      <div class="h-full bg-orange p-4 rounded-lg flex justify-center items-center text-xl font-semibold gap-1">
        <div class="h-[1.2rem] w-[1.2rem] flex items-center opacity-65">
          <img class=" h-full m-auto" src="./assets/search.svg">
        </div>
        <p class="hidden md:flex">
          search  
        </p>
        
      </div>
    </div>
    
    
  </div>
  
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
