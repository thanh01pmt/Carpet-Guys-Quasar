<template>
  <div class="main">
    <div class="mapContainer">
      <h4>Current Location:</h4><mapbox id="map" :access-token="mapboxToken" :map-options="mapOptions" @map-load="mapLoaded"></mapbox>
    </div>
  </div>
</template>

<script>
import Mapbox from 'mapbox-gl-vue'
export default {
  name: 'location',
  components: {
    'mapbox': Mapbox
  },
  methods: {
    mapLoaded (map) {
      let vue = this
      vue.map = map
      map.jumpTo({
        center: [vue.longitude, vue.latitude],
        zoom: 15
      })
    }
  },
  created () {
    let vue = this
    if (this.logged === false) {
      this.$router.push('/login')
    }
    navigator.geolocation.getCurrentPosition(locationSuccess, locationFail)
    function locationSuccess (position) {
      vue.latitude = position.coords.latitude
      vue.longitude = position.coords.longitude
      vue.altitude = position.coords.altitude
      vue.accuracy = position.coords.accuracy
      vue.altitudeAccuracy = position.coords.altitudeAccuracy
    }
    function locationFail () {
      alert('It seems we cant find you, please reload the page and try again.')
      this.locationError = true
    }
  },
  data: function () {
    return {
      map: {},
      longitude: 0,
      latitude: 0,
      altitude: 0,
      accuracy: 0,
      altitudeAccuracy: 0,
      mapboxToken: 'pk.eyJ1IjoiZ3JhcGV0b2FzdCIsImEiOiJjajhkeHR5YzEwdXp4MnpwbWhqYzI4ejh0In0.JzUlf5asD6yOa5XvjUF5Ag',
      mapOptions: {
        style: 'mapbox://styles/mapbox/streets-v9',
        center: [0, 0],
        zoom: 1
      }
    }
  }
}
</script>

<style >
#map {
  width: 100%;
  height: 300px;
  margin: 1.2%;
}

.mapContainer {

}

h4 {

}
</style>
