<template>
  <!-- Menggunakan div sebagai pembungkus utama -->
  <div class="background">
    <h1>RAMADHANUL IRFAN
    </h1> 
    <h2>NPM 223510935
    </h2>
    <!-- Menampilkan kegiatan yang sudah ada dalam sebuah tabel -->
    <table>
      <thead>
        <tr>
          <th>Kegiatan</th>
          <th>Status</th>
          <th>Tindakan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="activity in activities" :key="activity.id" :class="{ completed: activity.completed }">
          <td>
            <!-- Jika kegiatan sudah selesai, maka tampilkan dengan coretan -->
            <span :style="{ 'text-decoration': activity.completed ? 'line-through' : 'none' }">{{ activity.name }}</span>
          </td>
          <td>
            <!-- Jika kegiatan sudah selesai, tampilkan 'Telah Selesai', jika belum, tampilkan 'Belum Selesai' -->
            <span v-if="activity.completed">Telah Selesai</span>
            <span v-else>Belum Selesai</span>
            <input type="checkbox" v-model="activity.completed">
          </td>
          <td>
            <button @click="cancelActivity(activity.id)">Hapus</button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Form untuk menambahkan kegiatan baru -->
    <form @submit.prevent="addActivity">
      <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan baru">
      <button type="submit">Tambahkan</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Data contoh untuk kegiatan
const activities = ref([
  { id: 1, name: 'Kegiatan 1', completed: false },
  { id: 2, name: 'Kegiatan 2', completed: false }
]);

// Kolom input untuk kegiatan baru
const newActivity = ref('');

// Fungsi untuk menambahkan kegiatan baru
function addActivity() {
  if (newActivity.value.trim() !== '') {
    activities.value.push({ id: Date.now(), name: newActivity.value, completed: false });
    newActivity.value = '';
  }
}

// Fungsi untuk membatalkan kegiatan
function cancelActivity(id) {
  const index = activities.value.findIndex(activity => activity.id === id);
  if (index !== -1) {
    activities.value.splice(index, 1);
  }
}
</script>

<style>
  /* CSS untuk pembungkus utama */
.background {
    background-image: url(3.jpg);
    background-repeat: no-repeat;
    background-size: cover; /* Mengisi seluruh area latar belakang */
    min-height: 100vh; 
    padding: 20px;
    
}



  .completed {
    background-color: pink;
  }
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    border: 1px solid black;
    padding: 8px;
    text-align: left;
  }
  th {
    background-color: white;
  }

  /* Menambahkan coretan untuk kegiatan yang sudah selesai */
  .completed span {
    text-decoration: line-through;
  }
</style>
