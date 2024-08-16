<template>
    <div class="container">
      <h2 style="color: #3498db;">Fetched Data</h2>
      <ul>
        <li v-for="item in data" :key="item.id" :style="{ color: '#2ecc71', marginBottom: '8px' }">
          {{ item.name }}
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  
  export default {
    setup() {
      const data = ref([]);
  
      onMounted(async () => {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users');
          if (!response.ok) {
            throw new Error('%cFailed to fetch data', 'color: red; font-weight: bold;');
          }
          data.value = await response.json();
          console.log('%cData fetched successfully:', 'color: green; font-weight: bold;', data.value);
        } catch (error) {
          console.error('%cError:', 'color: red; font-weight: bold;', error);
        }
      });
  
      return { data };
    }
  };
  </script>
  
  <style scoped>
  .container {
    padding: 20px;
    background-color: #f4f4f4;
    border-radius: 8px;
    max-width: 600px;
    margin: 0 auto;
  }
  </style>
  