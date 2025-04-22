<script setup lang="ts">
import { ref, defineEmits } from 'vue';
import SearchButton from './SearchButton.vue';

const text = ref('');
const emit = defineEmits(['updateSearch', 'updateModal','deleteSearch']);
const props = defineProps({
  modal: {
    type: Boolean,
    default: false
  },
  previewImage: {
    type: String,
    default: ''
  },
})

function onInput(e) {
  text.value = e.target.value;
  console.log(text.value);
}

function onSearch(e) {
  emit('updateSearch', text.value); 
  
}

function onOpenModal(e) {
  emit('updateModal', true);
}

function onDelete(){
  text.value = '';
  emit('deleteSearch', '');
 
}


</script>

<template>
  <div class="h-full rounded-xl w-[50rem] bg-secondary overflow-hidden shrink border border-stone-800 flex flex-nowrap items-center">
    <div class="h-[60%] flex items-center mx-3 opacity-65">
      <img class="h-[80%] m-auto" src="../assets/search.svg">
    </div>

    <div @click="onOpenModal" v-if="props.previewImage" class="w-[2.2rem] h-[2.2rem] flex justify-center items-center cursor-pointer bg-secondary border border-orange mx-2 rounded-md shrink-0">
      <div class="h-full w-full flex items-center opacity-65 cursor-pointer">
        <img class="h-full w-full" :src="props.previewImage" v-if="props.previewImage">
      </div>
    </div>

    <input :value="text" @input="onInput"
      type="text" placeholder="Masukkan sesuatu... " class="p-2 text-xl outline-none w-full bg-secondary">


    <!-- this is image logo -->
    <div v-if="!text && !previewImage " @click="onOpenModal" class="w-[2.2rem] h-[2.2rem] flex justify-center items-center cursor-pointer bg-secondary border border-orange mx-2 rounded-md shrink-0">
      <div class="h-[1.2rem] w-[1.2rem] flex items-center opacity-65 cursor-pointer">
      <img class="h-full m-auto" src="../assets/image-logo.svg">
      </div>
    </div>
    <div v-if="text || previewImage"
     @click="onDelete" class="w-[2.2rem] h-[2.2rem] flex justify-center items-center cursor-pointer  rounded-md shrink-0">
      <div class="h-[1.2rem] w-[1.2rem] flex items-center opacity-65 cursor-pointer">
        <img class="h-[90%] m-auto" src="../assets/close-button.svg">
      </div>
    </div>

    <!-- this is button -->
    <SearchButton  @click="onSearch"></SearchButton>
  </div>
</template>

