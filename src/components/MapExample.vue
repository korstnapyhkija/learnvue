<template>
<div>
    <button class="button is-primary" @click="goToHome">Go to home</button>
    <!-- <google-maps :lat="this.lat" :lng="this.lng" :zoom="this.zoom"></google-maps> -->
    <leaflet-map :lat="lat" :lng="lng" :zoom="zoom"></leaflet-map>
</div>
</template>

<script>
import GoogleMaps from './GoogleMaps.vue'
import LeafletMap from './LeafletMap.vue'
export default {
  components: { GoogleMaps, LeafletMap },
    created(){
        let url = "https://raw.githubusercontent.com/johan/world.geo.json/master/countries.geo.json";
        axios.get(url).then(response =>{
            console.log(response.data);
            this.geoJson = response.data;
        });
    },
    data(){
        return {
            lat: 59.4265182,
            lng: 24.7431717,
            zoom: 18.25
        }
    },
    methods: {
        goToHome(){
            this.lat=59.4113121,
            this.lng=24.7031906,
            this.zoom=18
        }
    }
}
</script>

<style>

</style>