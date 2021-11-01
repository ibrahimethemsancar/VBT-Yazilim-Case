<template>
  <navBar />
  <container/>
</template>

<script>
import navBar from './components/navBar.vue'
import container from './components/container.vue'

export default {
  name: 'App',
  components: {
    navBar,
    container
  }
}
</script>

<style>
#app {
  
}
</style>
