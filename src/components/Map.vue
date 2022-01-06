<template>
    <div id="map"></div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Map, Control, CRS } from "leaflet";
import { GoogleMap, Tianditu, OSM } from "../lib/src/index";

const tdt = new Tianditu("cfcbc282308686d26782fcb4e11b32a4");
const osm = new OSM();
const googlemap = new GoogleMap();
const oStand = osm.stand();
const gSatellite = googlemap.satellite();
const 天地图影像 = tdt.img();
const 天地图矢量 = tdt.vec();
const 天地图注记 = tdt.cva();
const 影像注记 = tdt.cia();
const 天地图地形 = tdt.ter();
const 全球境界 = tdt.ibo();
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
            crs: CRS.EPSG3857,
        });
        let baseMaps = {
            OpenStreetMap: oStand,
            "Google Maps": gSatellite,
            天地图矢量,
            天地图影像,
            天地图地形,
        };
        let zhuji = {
            矢量注记: 天地图注记,
            影像注记,
            全球境界,
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
    height: 100vh;
}
</style>
