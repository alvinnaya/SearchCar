<template>
    <div v-if="isVisible"
      class="fixed w-full h-full z-[1000] flex items-center justify-center "
     
    >
      <div class="bg-white rounded-lg shadow-lg w-11/12 max-w-lg p-6 ">
        <button
          class="text-gray-500 hover:text-gray-800 float-right text-2xl font-bold"
          @click="closeModal"
          aria-label="Close"
        >
          &times;
        </button>
        <h2 class="text-xl font-semibold mb-4">Upload Image</h2>
        <form @submit.prevent="submitForm" class="space-y-4">
          <input
            type="file"
            @change="handleFileUpload"
            accept="image/*"
            required
            class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded file:border file:border-gray-300 file:text-sm file:font-semibold file:bg-gray-50 file:text-gray-700 hover:file:bg-gray-100"
          />
          <button
            type="submit"
            class="w-full bg-orange text-black py-2 px-4 rounded focus:outline-none focus:ring-2 focus:ring-blue-400 focus:ring-offset-2"
          >
            Search Image
          </button>
        </form>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  
  const props = defineProps<{
    isVisible: boolean;
    onClose: () => void;
  }>();
  
  const file = ref<File | null>(null);
  const emit = defineEmits(['data', 'vector']);
  const previewImage = ref('');
  
  function handleFileUpload(event: Event) {
    const target = event.target as HTMLInputElement;
    if (target.files && target.files.length > 0) {
      file.value = target.files[0];
      if (file.value) {
        const reader = new FileReader();
        reader.onload = () => {
          const base64String = reader.result as string;
          console.log('Base64 String:', base64String);
          previewImage.value = base64String; // Set the preview image
        };
        reader.readAsDataURL(file.value);
      }
    }
  }
  
  async function submitForm() {
    if (file.value) {
      try {
        // Buat FormData untuk mengirim file
        const formData = new FormData();
        formData.append('image', file.value);
  
        // Kirim permintaan POST ke API
        const response = await fetch('http://127.0.0.1:5000/get-vector', {
          method: 'POST',
          body: formData,
        });
  
        if (!response.ok) {
          throw new Error('Failed to upload image');
        }
        emit('data', previewImage.value);
        const result = await response.json();

  
        // Emit data hasil upload (jika diperlukan)
        emit('vector', result);
  
        // Tutup modal setelah upload berhasil
        props.onClose();
      } catch (error) {
        console.error('Error uploading image:', error);
      }
    }
  }
  
  function closeModal() {
    props.onClose();
  }
  </script>
  
  <style>
  /* No additional styles needed as Tailwind handles styling */
  </style>