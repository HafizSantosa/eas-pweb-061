<template>
    <div>
      <div v-for="submission in submissions" :key="submission.id" class="my- ">
        <h2>{{ submission.name }}</h2>
        <p>Email: {{ submission.email }}</p>
        <p>Institution: {{ submission.institution }}</p>
        <p>Status: {{ submission.status }}</p>
        <p>Date: {{ formatDate(submission.date) }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const submissions = ref([]);
  
  const fetchData = async () => {
    try {
      const response = await fetch('http://localhost:5000/api/submissions', {
        method: 'GET',
        credentials: 'include',
        headers: {
          'Content-Type': 'application/json',
        },
      });
  
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
  
      const responseData = await response.json();
      submissions.value = responseData.docs;
    } catch (err) {
      console.error(err);
      throw err;
    }
  };
  
  onMounted(async () => {
    try {
      await fetchData();
    } catch (error) {
      console.error(error);
      alert('Terjadi kesalahan saat mengambil data.');
    }
  });
  
  const formatDate = (dateString) => {
    const options = { year: 'numeric', month: 'long', day: 'numeric' };
    return new Date(dateString).toLocaleDateString(undefined, options);
  };
  </script>
  