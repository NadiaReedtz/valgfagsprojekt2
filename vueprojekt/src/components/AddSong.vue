<template>
  <form @submit.prevent="addSong">
    <input type="text" v-model="newSong.title" placeholder="Titel" required>
    <input type="text" v-model="newSong.artist" placeholder="Artist" required>
    <!-- Tilføj flere input-felter efter behov -->
    <button type="submit">Tilføj Sang</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      newSong: {
        title: '',
        artist: '',
        // andre felter
      },
      // Resten af din data...
    };
  },
  methods: {
    addSong() {
      this.songs.push(this.newSong);
      this.newSong = { title: '', artist: '' }; // Reset input felter
      // Her kunne du også tilføje logik til at persistere den nye sang i en database eller en lokal storage.
    },
  },
};
</script>
