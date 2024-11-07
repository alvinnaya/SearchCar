<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <div class="w-full min-h-screen flex flex-col justify-center items-center bg-main">
    <h1 class="text-5xl">Hello</h1>
    <div class="flex flex-nowrap px-4 gap-2 m-4 items-center md:h-[3rem] h-[3rem] w-full justify-center ">
      
     <!-- this is search bar -->
      <div class=" h-full bg-slate-300 rounded-xl w-[50rem] 
       bg-secondary overflow-hidden shrink border border-stone-800 flex flex-nowrap items-center">
        <div class="h-[60%] flex items-center mx-3 opacity-65">
          <img class=" h-[80%] m-auto" src="./assets/search.svg">
        </div>
  
        <input type="text" placeholder="Masukkan sesuatu... " class="p-2 text-xl outline-none w-full bg-secondary">

        <div class="w-[2.2rem] h-[2.2rem] flex justify-center items-center cursor-pointer bg-secondary border border-orange mx-2 rounded-md shrink-0">
          <div class="h-[1.2rem] w-[1.2rem] flex items-center opacity-65 cursor-pointer">
            <img class=" h-full m-auto" src="./assets/image-logo.svg">
          </div>
        </div>


        <!-- this is button -->
        <div class="h-[2.2rem] bg-orange p-2 m-2 rounded-lg flex justify-center items-center text-xl font-semibold gap-1">
        <div class="h-[1.2rem] w-[1.2rem] flex items-center opacity-65">
          <img class=" h-full m-auto" src="./assets/search.svg">
        </div>
        <p class="hidden md:flex cursor-pointer">
          search  
        </p>
        
      </div>
       

      </div>

      
    </div>
    
  </div>
  
</template>


