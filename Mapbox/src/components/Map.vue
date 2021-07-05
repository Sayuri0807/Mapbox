<template>
  <div id="map"></div>
</template>

<script lang="ts">
import Mapbox, { Control } from "mapbox-gl";
import { Component, Vue } from "vue-property-decorator";
@Component
export default class Map extends Vue {
  map?: Mapbox.Map = undefined;// ? pode ou não ter valor - ! variavél terá valor
  nav?: Control;
  markers = [];
  container = "map";
  accessToken =
    "pk.eyJ1Ijoic2F5dXJpMDgiLCJhIjoiY2txOXEyN3UzMDFuMjJvbGp3bWpiY3JnbSJ9.ACI53nLC52OHC4XNhQtaEg";// key
  mapStyle = "mapbox://styles/sayuri08/ckq9sror12jzk17lbqglyddik"; // estilo do mapa feito pelo mapbox
  zoom = 4;
  showCompass = true;
  showZoom = true;
  lat = -46.6388;
  lng = -23.5489;

  mounted(): void {
    Mapbox.accessToken = this.accessToken;
    this.map = new Mapbox.Map({
      container: this.container,
      style: this.mapStyle,
      center: [this.lat, this.lng],// onde o mapa irá ser centralizado no começo
      zoom: this.zoom,
    });
    this.nav = new Mapbox.NavigationControl({// adcionar controles de zoom e compasso 
      showCompass: this.showCompass,
      showZoom: this.showZoom,
    });
    this.map.addControl(this.nav, "top-left");// localização do controle de navegação
    new Mapbox.Marker({//adicionar marcador
      color: "#FF0000",
    })
      .setLngLat([this.lat, this.lng])
      .addTo(this.map);
  }
}
</script>

<style scoped>
#map {
  position: absolute;
  width: 100%;
  top: 0;
  bottom: 0;
}
</style>
