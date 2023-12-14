<template>
  <div>
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Nama:</label>
        <input id="name" v-model="submission.name" type="text" required />
      </div>
      <div>
        <label for="email">Email:</label>
        <input id="email" v-model="submission.email" type="email" required />
      </div>
      <div>
        <label for="institution">Asal Sekolah:</label>
        <input id="institution" v-model="submission.institution" type="text" required />
      </div>
      <div>
        <label for="date">Tanggal:</label>
        <input id="date" v-model="submission.date" type="date" required />
      </div>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const submission = ref({
      name: '',
      email: '',
      institution: '',
      status: 'waiting',
      date: '',
    });

    const submitForm = async () => {
      try {
        const response = await fetch('http://localhost:5000/api/submissions', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(submission.value),
        });

        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }

        alert('Data berhasil disimpan!');
        submission.value = {
          name: '',
          email: '',
          institution: '',
          status: 'waiting',
          date: '',
        };
      } catch (err) {
        console.error(err);
        alert('Terjadi kesalahan saat menyimpan data.');
      }
    };

    return {
      submission,
      submitForm,
    };
  },
};
</script>
