<template>
  <div class='photos'>
    <form v-on:submit.prevent='getPhotos'>
      <input type='text' id='search' v-model='search' placeholder='search for photos' />
      <img v-if='loading' src='https://primelinetools.com/pub/media/catalog/product/placeholder/default/ajax-loader02_5.gif' alt='loading circle' class='loading'>
    </form>
    <div class='photo-container'>
      <div v-for='photo in photos' v-bind:key='photo.display'>
        <a v-bind:href='photo.link' target='_blank'>
          <img v-bind:src='photo.display' class='photo'>
        </a>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Photos',
  data() {
    return {
      key: process.env.VUE_APP_ACCESS_KEY,
      loading: false,
      search: '',
      photos: []
    }
  },
  methods: {
    async getPhotos() {
      this.photos = [];
      this.loading = true;
      const url = `https://api.unsplash.com/search/photos?page=1&per_page=30&query=${this.search}&client_id=${this.key}`
      const response = await fetch(url);
      try {
        if(response.ok) {
          const photos = await response.json();
          this.cleanPhotos(photos.results);
        }
      } catch (err) {
        // console.log(err.message)
      }
      this.search = '';
      this.loading = false;
    },

    cleanPhotos (photos) {
      this.photos = photos.map(photo => ({display: photo.urls.regular, link: photo.links.html}))
    }
  }

}
</script>

<style scoped>

</style>


