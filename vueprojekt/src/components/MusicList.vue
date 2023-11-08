<template>
  <div class="search-container">
  <div class="search-box">
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
.music-list {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  text-align: center;
  color: #121A28;
  margin-top: 20px;
}


.search-container {
    display: grid;
    place-items: center;
    height: 60vh;
}

.search-box {
    width: 50%;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Rettet til korrekt CSS-syntaks */
    border-radius: 10px; 
    background: #ffffff; /* 'background' er nu stavet korrekt */
}


h1 {
  color: #121A28; 
}

input[type="text"] {
  border: 10px solid #bdc3c7;
  border-radius: 6px;
  padding: 10px;
  margin-bottom: 20px;
  width: 80%; 
}

ul {
  padding: 0;
  list-style: none;
}

li {
  background-color: #ecf0f1; 
  padding: 10px; 
  margin-bottom: 10px;
  margin-left: 200px;
  margin-right: 200px;
  border-radius: 4px;
  transition: background-color 0.3s ease; 
}

li:hover {
  background-color: #d0d3d4; 
}
</style>
