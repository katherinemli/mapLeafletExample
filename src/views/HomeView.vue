<template>
  <div class="home">
    <HelloWorld msg="Katherine Liberona, Full Stack Developer"/>
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
