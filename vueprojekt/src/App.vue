<template>
  <div id="app">
    <!-- Andre komponenter eller indhold her -->
    <music-list></music-list>
  </div>
</template>

<script>
import MusicList from '@/components/MusicList.vue';


export default {
  name: 'App',
  components: {
    MusicList // Det her er shorthand for MusicList: MusicList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
