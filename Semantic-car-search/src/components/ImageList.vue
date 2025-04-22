<script setup lang="ts">
import SearchButton from './SearchButton.vue';
import { onMounted, ref, watch } from 'vue'

const isThrottling = ref(false);
const data = ref<any[]>([]);
const page = ref<number>(2);
const url = ref<string>("https://api.pexels.com/v1/curated?")
const isGetData = ref<boolean>(false)
const props = defineProps(['searchQuery','data']);
const emit = defineEmits(['getInitialData','getNewData']);

const getMoreData = async ()=>{
    isGetData.value =await true;
    console.log("start mount :",data.value.length)
    emit('getNewData', page.value)
  
page.value = await page.value + 1;
isGetData.value = await false;


}

function addSscroll(){

     // Mendapatkan tinggi total halaman
     const totalHeight = document.documentElement.scrollHeight - window.innerHeight;
      // Mendapatkan posisi scroll saat ini
      const scrollPosition = window.scrollY;
      const scrollPercentage = Math.round((scrollPosition / totalHeight) * 100);
      if(scrollPercentage >= 95 && !isGetData.value){
        getMoreData();
        
      }
   
}

 function scrollTimeout(){

    if(isThrottling.value){
        return;
    }

    isThrottling.value = true;
    addSscroll();
   

    setTimeout(() => {
        isThrottling.value = false;
      }, 100); // Waktu interval throttling 100ms


 }

onMounted(async() => {
  // component is now mounted.
  
  console.log("start mount")
  isGetData.value = true;
  emit('getNewData', 0)
  isGetData.value = false;


  window.addEventListener('scroll', scrollTimeout);
 
   
  

})



</script>

<template>
    <div class=" w-full p-2 m-auto ">
      <h1 class="text-3xl text-center font-semibold">{{ searchQuery }}</h1>
        <div :style="`grid-template-rows: repeat(${data.values.length}, minmax(0, 1fr));`"
        :class=" `grid col-span-1 bg-secondary gap-2  items-center
        lg:grid-cols-5 md:grid-cols-4 sm:grid-cols-3 grid-cols-2`">

            <!-- list of images -->
              
               
               
                <img v-for="(item, index) in props.data" :key="item.payload.id" :src="`http://127.0.0.1:5000/get-image/${item.payload.id}.jpg`"
                :class="`w-full col-span-1 bg-no-repeat my-2  m-2 rounded-lg row-start-auto
                `">
    
 
        </div>

    </div>
</template>


<style>
.Modgrid {
    display: grid;
  grid-gap: 10px;
  grid-template-columns: repeat(auto-fill, minmax(250px,1fr));
  grid-auto-rows: 20px;
}
</style>

