<script setup lang="ts">
import SearchButton from './SearchButton.vue';
import { ref } from 'vue'


const text = ref('')

function onInput(e) {
  // a v-on handler receives the native DOM event
  // as the argument.
  text.value = e.target.value
  console.log(text.value)
}

</script>

<template>
      <div class=" h-full bg-slate-300 rounded-xl w-[50rem] 
       bg-secondary overflow-hidden shrink border border-stone-800 flex flex-nowrap items-center">
        <div class="h-[60%] flex items-center mx-3 opacity-65">
          <img class=" h-[80%] m-auto" src="../assets/search.svg">
        </div>
  
        <input :value="text" @input="onInput"
         type="text" placeholder="Masukkan sesuatu... " class="p-2 text-xl outline-none w-full bg-secondary">

        <!-- this is image logo -->
        <div class="w-[2.2rem] h-[2.2rem] flex justify-center items-center cursor-pointer bg-secondary border border-orange mx-2 rounded-md shrink-0">
          <div class="h-[1.2rem] w-[1.2rem] flex items-center opacity-65 cursor-pointer">
            <img class=" h-full m-auto" src="../assets/image-logo.svg">
          </div>
        </div>


        <!-- this is button -->
        <SearchButton></SearchButton>
       

      </div>
</template>

