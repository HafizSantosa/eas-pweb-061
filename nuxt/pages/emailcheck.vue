<template>
    <div>
      <form @submit.prevent="checkStatus">
        <div>
          <label for="email">Email:</label>
          <input id="email" v-model="email" type="email" required />
        </div>
        <button type="submit">Check Status</button>
      </form>
      <div v-if="status">
        <h2>Status: {{ status }}</h2>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      const email = ref('');
      const status = ref(null);
  
      const checkStatus = async () => {
        try {
          const response = await fetch(`http://localhost:5000/api/submissions?email=${email.value}`, {
            method: 'GET',
            headers: {
              'Content-Type': 'application/json',
            },
          });
  
          if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
          }
  
          const responseData = await response.json();
          if (responseData.docs && responseData.docs.length > 0) {
            status.value = responseData.docs[0].status;
          } else {
            alert('Email tidak ditemukan.');
          }
        } catch (err) {
          console.error(err);
          alert('Terjadi kesalahan saat memeriksa status.');
        }
      };
  
      return {
        email,
        status,
        checkStatus,
      };
    },
  };
  </script>
  