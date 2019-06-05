<template>
  <div class='homepage'>
    <Header />
    <Photos />
  </div>
</template>

<script>
import Header from './Header';
import Photos from './Photos';

export default {
  name: 'HomePage',
  components: {
    Header,
    Photos
  }
}
</script>
