<template>
    <div id="map"></div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Map, Control } from "leaflet";
import { GoogleMap, Tianditu, OSM } from "../lib/src/index";

const tdt = new Tianditu("cfcbc282308686d26782fcb4e11b32a4");
const osm = new OSM();
const googlemap = new GoogleMap();
const oStand = osm.stand();
const gSatellite = googlemap.satellite();
const 天地图注记 = tdt.cva_w();
const 天地图矢量 = tdt.vec_w();

export default defineComponent({
    name: "Map",
    data() {
        return {};
    },
    methods: {},
    mounted() {
        const map = new Map("map", {
            center: [35, 115],
            zoom: 10,
            layers: [gSatellite, 天地图注记],
        });
        let baseMaps = {
            OpenStreetMap: oStand,
            "Google Mpas": gSatellite,
            天地图矢量,
        };
        let zhuji = {
            天地图注记: 天地图注记,
        };
        let ctrl = new Control.Layers(baseMaps, zhuji, { collapsed: false });
        ctrl.addTo(map);
        let scale = new Control.Scale({ imperial: false });
        scale.addTo(map);
    },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "~leaflet/dist/leaflet.css";
#map {
    width: 100%;
    height: 500px;
}
</style>
