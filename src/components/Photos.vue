<template>
  <div>
    <form v-on:submit.prevent='getPhotos'>
      <input type='text' id='search' v-model='searchInput' placeholder='search for photos' />
    </form>
    <img v-if='loading' src='https://primelinetools.com/pub/media/catalog/product/placeholder/default/ajax-loader02_5.gif' alt='loading circle' class='loading'>
    <PhotoContainer :photos='photos' />
  </div>
</template>

<script>
import PhotoContainer from './PhotoContainer';

export default {
  name: 'Photos',
  data() {
    return {
      key: process.env.VUE_APP_APIKEY,
      loading: false,
      searchInput: '',
      photos: []
    }
  },
  methods: {
    async getPhotos() {
      this.photos = [];
      this.loading = true;
      const url = `https://api.unsplash.com/search/photos?page=1&per_page=30&query=${this.searchInput}&client_id=${this.key}`
      const response = await fetch(url);
      try {
        if(response.ok) {
          const photos = await response.json();
          this.selectPhotos(photos.results);
        }
      } catch (err) {
        return err;
      }
      this.searchInput = '';
      this.loading = false;
    },

    selectPhotos (photos) {
      this.photos = photos.map(photo => ({display: photo.urls.regular, link: photo.links.html}))
    }
  },
  components: {
    PhotoContainer
  }

}
</script>

<style scoped>
  input {
    border: 1px solid #CCC;
    border-radius: 50px;
    border-style: solid;
    font-size: 1.5em;
    margin-top: 20px;
    padding: 8px;
    padding-left: 15px;
    outline: none;
    width: 500px;
  }
</style>


