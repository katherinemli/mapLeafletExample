<template>
  <div>
    <div>
      <p>
        Change the values to play with the map.
      </p>
      <ul>
        <li>
          <div>Amount of points</div>
          <div>
            <input @input="emitEvent" @keypress="onlyNumberImput($event)" type="text" v-model.number="config.field1" />
          </div>
        </li>
      </ul>
    </div>
    <div style="height: 1000px; width: 100%">
      {{ dataFromChildOne }}
      <l-map v-if="showMap" :zoom="zoom" :center="center" :options="mapOptions" style="height: 80%"
        @update:center="centerUpdate" @update:zoom="zoomUpdate">
        <l-tile-layer :url="url" :attribution="attribution" />
        <l-marker v-for="marker in markers" :key="marker.id + '-mark'" :lat-lng="latLng(marker.lat, marker.long)">
          <!-- <l-tooltip :options="{ permanent: true, interactive: true }"> -->
          <l-tooltip :options="{ permanent: false, interactive: true }">
            <div @click="innerClick">
              {{ marker.location }}
              <p v-show="showParagraph">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
                sed pretium nisl, ut sagittis sapien. Sed vel sollicitudin nisi.
                Donec finibus semper metus id malesuada.
              </p>
            </div>
          </l-tooltip>
          <l-icon :icon-url="customMarker"></l-icon>
          <l-popup>
            <div @click="innerClick">
              I am a popup {{ marker }}
              {{ marker.lat }}
              {{ marker.long }}
              <p v-show="showParagraph">

              </p>
            </div>
          </l-popup>
        </l-marker>
        <!--       <l-marker :lat-lng="withTooltip">
        <l-icon :icon-url="customMarker"></l-icon>
        <l-tooltip :options="{ permanent: true, interactive: true }">
          <div @click="innerClick">
            I am a tooltip
            <p v-show="showParagraph">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
              sed pretium nisl, ut sagittis sapien. Sed vel sollicitudin nisi.
              Donec finibus semper metus id malesuada.
            </p>
          </div>
        </l-tooltip>
      </l-marker> -->
      </l-map>
    </div>
  </div>
</template>
  
<script>
import L from 'leaflet';
import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker, LPopup, LTooltip, LIcon } from "vue2-leaflet";
import 'leaflet/dist/leaflet.css';
import customMarker from '../assets/iconsLocation.png';
import {
  Icon
} from 'leaflet';
delete Icon.Default.prototype._getIconUrl;
Icon.Default.mergeOptions({
  iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
  iconUrl: require('leaflet/dist/images/marker-icon.png'),
  shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
});
export default {
  name: "MapLeaflet",
  props: ['dataFromChildOne'],
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LTooltip,
    LIcon
  },
  data() {
    return {
      config: {
        field1: 5,
        field2: '',
      },
      configFromBackend: {
        field1: 5,
        field2: 6,
      },
      customMarker,
      zoom: 13,
      center: latLng(40.724634757833414, -74.00701717096757),
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      withPopup: latLng(47.41322, -1.219482),
      withTooltip: latLng(47.41422, -1.250482),
      currentZoom: 11.5,
      currentCenter: latLng(40.724634757833414, -74.00701717096757),
      showParagraph: false,
      mapOptions: {
        zoomSnap: 0.5
      },
      showMap: false,
      markers: [],
      fullPath: '/createRoute/'
    };
  },

  methods: {
    latLng: function (lat, lng) {
      //console.log('latLng:', L.latLng(lat, lng))
      return L.latLng(lat, lng);
    },
    onlyNumberImput(evt) {
      if (Number(`${this.config.field1}${evt.key}`) > 683) {
        evt.preventDefault();
      }
      const charCode = evt.which ? evt.which : evt.keyCode;
      if (charCode > 31 &&
        (charCode < 48 || charCode > 57 || charCode == 46)

      ) {

        evt.preventDefault();
      }
    },
    initRequest() {
      //console.log(this.fullPath)
      var url = (this.config.field1 >= 1) ? `${this.fullPath}${this.config.field1}` : `${this.fullPath}1`
      this.axios.get(url)
        .then(response => {
          //console.log(response.data);
          this.markers = response.data;
          this.showMap = true;
          //this.markers = this.markers.slice(2, 3)

        })
        .catch(function (error) {
          console.log(error);
        });


    },
    emitEvent() {
      this.initRequest();
    },
    zoomUpdate(zoom) {
      this.currentZoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
    showLongText() {
      this.showParagraph = !this.showParagraph;
    },
    innerClick() {
      alert("Click!");
    },
  },
  created() {
    //this.initRequest();

  },
  mounted() {
    this.initRequest();


  },
};
</script>
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
