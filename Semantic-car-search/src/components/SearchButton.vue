<script setup lang="ts">
import { ref } from 'vue';


</script>

<template>
  <div
    class="h-[2.2rem] bg-orange p-2 m-2 rounded-lg flex justify-center items-center text-xl font-semibold gap-1 cursor-pointer"
   
  >
    <div class="h-[1.2rem] w-[1.2rem] flex items-center opacity-65">
      <img class="h-full m-auto" src="../assets/search.svg" />
    </div>
    <p class="hidden text-md md:flex text-[1rem]">
      search
    </p>
  </div>
</template>

