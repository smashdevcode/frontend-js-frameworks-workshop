<template>
  <div>
    <h2>{{ album.title }}</h2>
    <button v-on:click="viewDetails">View Details</button>
  </div>
</template>

<script>
export default {
  name: 'Album',
  props: ['album'],
  methods: {
    viewDetails() {
      this.$emit('view-details', this.album.id);
    }
  }
}
</script>

<style scoped>
</style>
