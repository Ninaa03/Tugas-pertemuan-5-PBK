<script setup>
import { ref, computed, watch, onMounted } from 'vue';

// **List Rendering - v-for**
// Data musik berdasarkan genre 
const songs = ref({
  "dream-pop": [
    "black beauty", "Blue Jeans", "Summertime Sadness", "West Coast", "Love"
  ],
  "alternative": [
    "Ride", "Brooklyn Baby", "Ultraviolence", "Hope is a Dangerous Thing"
  ],
  "cinematic": [
    "Young and Beautiful", "Dark Paradise", "13 Beaches", "Old Money"
  ],
  "folk": [
    "Let Me Love You Like a Woman", "White Dress", "Chemtrails Over the Country Club"
  ]
});

// Reaktif variabel
const selectedGenre = ref("");
const newSong = ref(""); // Input musik baru

// **Computed Properties - Hitung jumlah musik**
const songCount = computed(() => {
  return selectedGenre.value ? songs.value[selectedGenre.value].length : 0;
});

// **Watchers - Memonitor perubahan genre yang dipilih**
watch(selectedGenre, (newVal, oldVal) => {
  console.log(`Genre berubah dari "${oldVal}" ke "${newVal}"`);
});

// **Template Ref & Lifecycle Hook**
const genreSelect = ref(null);

onMounted(() => {
  if (genreSelect.value) {
    genreSelect.value.focus();
  }
});

// Fungsi untuk menambahkan musik ke genre yang dipilih
const addSong = () => {
  if (selectedGenre.value && newSong.value.trim() !== "") {
    songs.value[selectedGenre.value].push(newSong.value.trim());
    newSong.value = ""; // Reset input setelah menambahkan musik
  }
};
</script>

<template>
  <div class="container">
    <h1>Lana Del Rey</h1>

    <!-- Pilih Genre Musik -->
    <label for="genre">Pilih Genre Musik:</label>
    <select v-model="selectedGenre" id="genre" ref="genreSelect">
      <option disabled value="">-- Pilih Genre --</option>
      <option v-for="(songList, key) in songs" :key="key" :value="key">
        {{ key.toUpperCase() }}
      </option>
    </select>

    <div v-if="selectedGenre">
      <h3>Daftar Musik ({{ songCount }} musik):</h3>

      <!-- List Rendering - v-for daftar musik berdasarkan genre -->
      <ol>
        <li v-for="(song, index) in songs[selectedGenre]" :key="index">
          {{ song }}
        </li>
      </ol>

      <!-- Form Tambah Musik -->
      <div class="add-song">
        <input v-model="newSong" placeholder="Tambah musik baru..." />
        <button @click="addSong">Tambah Musik</button>
      </div>
    </div>
  </div>

  <h6>SERI MEHULINA BR SINULINGGA</h6>
  <h6>233510650</h6>
</template>

<style scoped>
.container {
  text-align: center;
  background-color: #f5f5f5;
  padding: 20px;
  font-family: Arial, sans-serif;
}
select, button, input {
  margin: 10px;
  padding: 5px;
}
.add-song {
  margin-top: 10px;
}
</style>
