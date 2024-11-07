<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import ImageList from './components/ImageList.vue';
import SearchBar from './components/SearchBar.vue';
import SearchButton from './components/SearchButton.vue';
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>

  <div class="flex flex-col justify-center">
    <div class="w-full min-h-[65vh] flex flex-col justify-end mb-20 items-center bg-main">
    <h1 class="text-5xl">Hello</h1>
    <div class="flex flex-nowrap px-4 gap-2 m-4 items-center md:h-[3rem] h-[3rem] w-full justify-center ">
     <!-- this is search bar -->
      <SearchBar></SearchBar>
    </div>
    
  </div>

  <ImageList>
    
  </ImageList>
  </div>
  
  
</template>


