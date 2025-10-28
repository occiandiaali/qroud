<template>
  <ion-page>
    <ion-header :translucent="true"> </ion-header>
    <ion-content :fullscreen="true">
      <ion-fab slot="fixed" vertical="top" horizontal="end" id="fab">
        <ion-fab-button @click="showAddReviewModal = false">
          <ion-icon :icon="chevronDownCircleOutline"></ion-icon>
        </ion-fab-button>
        <ion-fab-list side="bottom">
          <ion-fab-button>
            <ion-icon :icon="document"></ion-icon>
          </ion-fab-button>
          <ion-fab-button @click="setReviewModal(true)">
            <ion-icon :icon="add"></ion-icon>
          </ion-fab-button>
          <ion-fab-button>
            <ion-icon :icon="globe"></ion-icon>
          </ion-fab-button>
        </ion-fab-list>
      </ion-fab>
      <div id="container">
        <div id="mapContainer"></div>
      </div>
      <AddReviewModalComponent :openModal="showAddReviewModal" />
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
//import "leaflet/dist/leaflet.css";
import L, { LatLngExpression } from "leaflet";

import { onMounted, ref } from "vue";
import {
  IonFab,
  IonFabButton,
  IonFabList,
  IonHeader,
  IonContent,
  IonPage,
  IonIcon,
} from "@ionic/vue";
import { add, chevronDownCircleOutline, document, globe } from "ionicons/icons";

import AddReviewModalComponent from "@/components/AddReviewModalComponent.vue";

const showAddReviewModal = ref(false);

const centre = ref<LatLngExpression>([6.6969, 3.4197]);
const zoom = ref(13);

const setupLeafletMap = () => {
  const mapDiv = L.map("mapContainer").setView(centre.value, zoom.value);
  L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution:
      '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
    maxZoom: 18,
  }).addTo(mapDiv);
};

const setReviewModal = (open: boolean) => {
  showAddReviewModal.value = open;
};

onMounted(() => {
  setupLeafletMap();
  setTimeout(function () {
    window.dispatchEvent(new Event("resize"));
  }, 500);
});
</script>

<style lang="css" scoped>
#fab {
  z-index: 1000;
}
#mapContainer {
  width: 100%;
  height: 100vh;
}
</style>
