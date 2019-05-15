<template>
  <div>
    <navigation />
    <nuxt />
  </div>
</template>

<script>
import Navigation from '~/components/Navigation.vue'

export default {
  components: {
    Navigation
  }
}
</script>

<style>
  .masthead {
    background-image: url('../assets/img/about-bg.jpg') !important;
  }
</style>
