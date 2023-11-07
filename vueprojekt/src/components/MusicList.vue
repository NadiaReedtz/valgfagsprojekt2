<template>
  <div>
    <h1>Musikliste</h1>
    <input v-model="search.artist" placeholder="Søg efter artist">
    <input v-model="search.album" placeholder="Søg efter album">
    <input v-model="search.year" placeholder="Søg efter år">
    <input v-model="search.genre" placeholder="Søg efter genre">

    <ul v-if="isSearchActive">
      <li v-for="song in filteredMusic" :key="song.id">
        {{ song.artist }} - {{ song.album }} ({{ song.year }}) - {{ song.genre }}
      </li>
    </ul>
  </div>
</template>

<script>
import musicData from '@/data.json';

export default {
  name: 'MusicList',
  data() {
    return {
      musicData,
      search: {
        artist: '',
        album: '',
        year: '',
        genre: ''
      }
    };
  },
  computed: {
    filteredMusic() {
      return this.musicData.filter((song) => {
        return (
          (this.search.artist ? song.artist.toLowerCase().includes(this.search.artist.toLowerCase()) : true) &&
          (this.search.album ? song.album.toLowerCase().includes(this.search.album.toLowerCase()) : true) &&
          (this.search.year ? song.year.toString().includes(this.search.year) : true) &&
          (this.search.genre ? song.genre.toLowerCase().includes(this.search.genre.toLowerCase()) : true)
        );
      });
    },
    isSearchActive() {
      // Check if any search field is filled
      return Object.values(this.search).some(v => v !== '');
    }
  }
};
</script>

<style scoped>

</style>
