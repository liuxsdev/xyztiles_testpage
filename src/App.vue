<template>
    <Map />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Map from "./components/Map.vue";

export default defineComponent({
    name: "App",
    components: {
        Map,
    },
});
</script>

<style></style>
