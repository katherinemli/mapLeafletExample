<template>
  <div class="home">
    <HelloWorld msg="Katherine Liberona, Full Stack Developer"/>
      <MapLeaflet :data-from-child-one="dataFromChildOne"/>    
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
import MapLeaflet from '@/components/Map.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    MapLeaflet,
  },
  data() {
    return {
      dataFromChildOne: null
    };
  },
  methods: {
    handleEventFromChildOne(payload) {
      this.dataFromChildOne = payload;
    }
  }
}
</script>
<style>
.mapContainer{
  display: flex;
  flex-direction: row;
}
</style>
