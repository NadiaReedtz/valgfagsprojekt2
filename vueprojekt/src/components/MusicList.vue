<template>
  <div class="search-container">
  <div class="search-box">
    <h1>MUSIKLISTE</h1>
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

<style>
html, body {
  margin: 0;
  padding: 0;
  overflow: hidden; /* Forhindrer scrolling på hele siden */
  height: 100%; /* Sætter højden på siden til 100% af viewport-højden */
}

.search-container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start; /* Start alignment i stedet for center */
  align-items: center;
  height: 100vh;
  overflow: hidden;
  padding-top: 12%; /* Skubber søgeboksen ned fra toppen */
}


.search-box {
  width: 50%;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 10px; 
  background: #ffffff; 
}

h1 {
  color:  #202020;
}

input[type="text"] {
  border: 2px solid #bdc3c7;
  border-radius: 6px;
  padding: 10px;
  margin-bottom: 20px;
  width: calc(100% - 44px); /* Tilpasser bredden efter padding og border */
}

ul {
  padding: 0;
  list-style: none;
  margin: 0; /* Fjerner standardmargen */
}

li {
  background-color: #ecf0f1;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 4px;
  transition: background-color 0.3s ease;
  width: calc(100% - 40px); /* Tilpasser bredden til padding */
}

li:hover {
  background-color: #d0d3d4;
}

</style>
