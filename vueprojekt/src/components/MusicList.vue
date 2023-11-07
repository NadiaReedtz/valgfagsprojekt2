<template>
  <div>
    <h1>Musikliste</h1>
    <ul>
      <li v-for="item in musicData" :key="item.id">
        {{ item.artist }} - {{ item.album }} ({{ item.year }})
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
      musicData
    };
  }
};
</script>

<style scoped>
/* Her kan du tilføje CSS for din komponent */
</style>
