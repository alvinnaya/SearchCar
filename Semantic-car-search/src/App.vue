<script setup lang="ts">
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import ImageList from './components/ImageList.vue';
import SearchBar from './components/SearchBar.vue';
import SearchButton from './components/SearchButton.vue';
import ModalForm from './components/ModalForm.vue';

const searchQuery = ref('aircraft');
const isModalVisible = ref(false);
const data = ref<any[]>([]);
const previewImage = ref<string | undefined>(undefined);
const Vectordata = ref<any[]>([]);
const VectorCache = ref<any[]>([]);

function handleSearchUpdate(query) {
  searchQuery.value = query;
  ChangeData()
 
}
function handleCloseModal() {
  isModalVisible.value = false;
}

function handleOpenModal() {
  isModalVisible.value = true;
}

function handleModalData(data) {
  console.log("previwe",data);
  previewImage.value = data;
}


async function handlevector(data) {
  console.log("previwe",data);
  Vectordata.value = data;
  VectorCache.value = data;
  
  isModalVisible.value = false;

}
function handleDeleteImage(e) {
  previewImage.value = undefined;
  console.log("delete image",e)
  searchQuery.value = 'aircraft';
  Vectordata.value = []
}

const getNewData = async (page)=>{
  console.log("get new data",searchQuery.value,Vectordata.value)

  if(VectorCache.value.length > 0){
    const url = `http://127.0.0.1:5000/search-vectors?page=${page}`;
    console.log("fullUrl", url)
    const res = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(VectorCache.value),
    });
  const newdata = await res.json()
  console.log("initial Data", newdata)
  data.value = data.value.concat(newdata)

  }else{
    const fullUrl = `http://127.0.0.1:5000/cari?q=${searchQuery.value}&page=${page}`;
  console.log("fullUrl", fullUrl)
  const res = (await fetch(fullUrl,{
    method: 'GET',
    headers: {
            'Content-Type': 'application/json',
           
          }
  }))
  const newdata = await res.json()
  console.log("initial Data", newdata)
  data.value = data.value.concat(newdata)

  }
 

}

const ChangeData = async ()=>{
  console.log("get new data",Boolean(Vectordata.value))
  if(Vectordata.value.length > 0){
    const url = `http://127.0.0.1:5000/search-vectors?page=0`;
    console.log("fullUrl", url)
    const res = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(Vectordata.value),
    });
    const newdata = await res.json()
    console.log("initial Data", newdata)
    data.value = newdata
  }else{
    const fullUrl = `http://127.0.0.1:5000/cari?q=${searchQuery.value}&page=0`;
  console.log("fullUrl", fullUrl)
  const res = (await fetch(fullUrl,{
    method: 'GET',
    headers: {
            'Content-Type': 'application/json',
           
          }
  }))
  const newdata = await res.json()
  console.log("initial Data", newdata)
  data.value = newdata
  VectorCache.value = []
  }
  


}

</script>

<template>
  <ModalForm :isVisible="isModalVisible" @close="handleCloseModal" 
  @data="handleModalData" @vector="handlevector"></ModalForm>

  <div class="flex flex-col justify-center ">
   
    <div class="w-full min-h-[65vh] flex flex-col justify-end mb-20 items-center ">
    <h1 class="text-5xl ">Hello</h1>
    <div class="flex flex-nowrap px-4 gap-2 m-4 items-center md:h-[3rem] h-[3rem] w-full justify-center ">
     <!-- this is search bar -->
      <SearchBar @updateSearch="handleSearchUpdate" :modal = "isModalVisible" 
      @updateModal="handleOpenModal" :previewImage = "previewImage" @deleteSearch = "handleDeleteImage"></SearchBar>
    </div>
    
  </div>

  <ImageList :searchQuery = "searchQuery" @getNewData = "getNewData"  :data = "data" >
    
  </ImageList>

    

  </div>
  
  
</template>


