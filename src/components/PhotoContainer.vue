<template>
  <div class='photo-container'>
    <div v-for='photo in photos' v-bind:key='photo.display' class='photo-card'>
      <a v-bind:href='photo.link' target='_blank'>
        <div class='photo' :style="{ backgroundImage: `url('${photo.display}')` }"></div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PhotoContainer',
  props: ['photos']
}
</script>

<style scoped>
  .photo-container {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    padding: 1em;
    justify-content: center;
  }
  .photo {
    width: 100%;
    height: 400px;
    background-size: cover;
    background-position: top center;
    border-radius: 2px;
    box-shadow: 0 0 6px 2px #00000036;
  }
  .photo-card {
    display: flex;
    width: 31%;
    margin: 1%;
  }
  a {
    width: 100%;
  }
</style>

