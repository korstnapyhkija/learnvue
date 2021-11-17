<template>
  <div id="map"></div>
</template>

<script>
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';

export default {
    props: ['lat','lng','zoom','geoJson'],
    mounted(){
        this.map = L.map('map').setView([this.lat, this.lng], this.zoom);
        L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
            attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
            maxZoom: 18,
            id: 'mapbox/streets-v11',
            tileSize: 512,
            zoomOffset: -1,
            accessToken: "pk.eyJ1Ijoia29yc3RuYXB5aGtpamEiLCJhIjoiY2t3MzdxYjB5MjJsaDJucWlndTFyMTY1ciJ9.Ei9oRvvv8ADJqR00Lcnfqw"
        }).addTo(this.map);
            L.geoJson(this.geoJson).addTo(this.map);
    },
    data(){
        return{
            map:null
        }
    },
    watch: {
        lat(lat){
            this.map.flyTo([lat, this.lng], this.zoom);
        },
        lng(lng){
            this.map.flyTo([this.lat, lng], this.zoom);
        },
        zoom(zoom){
            this.map.flyTo([this.lat, this.lng], zoom);
        },
        geoJson(geoJson){
            L.geoJson(this.geoJson).addTo(this.map);
        }
    }
}
</script>

<style>
    #map { 
        height: 800px; }
</style>