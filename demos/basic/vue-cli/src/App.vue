<template>
  <div id="app">
    <album v-for="album in albums" 
      v-bind:album="album" 
      v-bind:key="album.id"
      v-on:view-details="handleViewDetails"></album>
  </div>
</template>

<script>
import Album from './components/Album.vue'

export default {
  name: 'app',
  data: function() {
    return {
      albums: []
    };
  },
  components: {
    Album
  },
  methods: {
    handleViewDetails(albumId) {
      alert(`View details! (Album ID: ${albumId})`);
    }
  },
  created() {
    fetch('http://localhost:3000/albums')
      .then(response => response.json())
      .then(data => this.albums = data);
  }
}
</script>

<style>
</style>
