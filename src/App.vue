<template>
  <div id="app">
    <Header/>
    <div class="container">
      <AlbumCardContainer />
    </div>
  </div>
</template>

<script>
import AlbumCardContainer from './components/AlbumCardContainer.vue';
import Header from './components/Header.vue';

export default {
  name: "App",
  components: {AlbumCardContainer, Header},
};
</script>

<style lang="scss">
@import "@/styles/app.scss";
</style>
