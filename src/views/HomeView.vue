<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <MapLeaflet msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import MapLeaflet from '@/components/Map.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    MapLeaflet
  }
}
</script>
