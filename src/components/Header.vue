<template>
  <FixedHeader>
    <header class='navbar'>
      <h1>Photo Searcher</h1>
    </header>
  </FixedHeader>
</template>

<script>
import FixedHeader from 'vue-fixed-header';
export default {
  name: 'Header',
  components: {
    FixedHeader
  }
}
</script>

<style scoped>
  .navbar {
    background: #000;
    color: #FFF;
    text-align: center;
    padding: 10px;
  }
  .navbar.vue-fixed-header--isFixed {
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
}
</style>
