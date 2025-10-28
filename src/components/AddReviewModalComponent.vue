<template>
  <ion-modal
    ref="modal"
    :is-open="openModal"
    v-on:did-dismiss="!openModal"
    :initial-breakpoint="0.25"
    :breakpoints="[0, 0.25, 0.5, 1]"
  >
    <ion-content class="ion-padding">
      <!-- <ion-item>
        <ion-label>
          <h2>Modal content</h2>
        </ion-label>
      </ion-item> -->
      <div class="form-div">
        <ion-item>
          <ion-input
            label="Location name"
            label-placement="floating"
            placeholder="The name of the area.."
          ></ion-input>
        </ion-item>
        <ion-item>
          <ion-input
            label="Business name"
            label-placement="floating"
            placeholder="The name of the business.."
          ></ion-input>
        </ion-item>
        <ion-item>
          <ion-textarea
            label="Review"
            label-placement="floating"
            placeholder="Your review of the place.."
          ></ion-textarea>
        </ion-item>
        <ion-item>
          <ion-label>Rate it</ion-label>
          <ion-icon :icon="starOutline"></ion-icon>
          <ion-icon :icon="starOutline"></ion-icon>
          <ion-icon :icon="starOutline"></ion-icon>
          <ion-icon :icon="starOutline"></ion-icon>
          <ion-icon :icon="starOutline"></ion-icon>
        </ion-item>
        <ion-item button @click="openFileDialog">
          <ion-label>Select File</ion-label>
          <!-- <input type="file" ref="fileInput" @change="handleFileChange" style="display: none;" /> -->
        </ion-item>
      </div>
    </ion-content>
  </ion-modal>
</template>

<script setup lang="ts">
import { ref } from "vue";
import {
  IonButton,
  IonModal,
  IonHeader,
  IonIcon,
  IonContent,
  IonTextarea,
  IonToolbar,
  IonTitle,
  IonItem,
  IonInput,
  IonList,
  IonAvatar,
  IonImg,
  IonLabel,
  IonSearchbar,
} from "@ionic/vue";
import { starOutline } from "ionicons/icons";

const fileInput = ref();
const selectedFile = ref(null);

const props = defineProps(["openModal"]);

const openFileDialog = () => {
  fileInput.value?.click();
};

const handleFileChange = (event: { target: { files: null[] } }) => {
  selectedFile.value = event.target.files[0];
};

const uploadFile = () => {
  if (selectedFile.value) {
    const formData = new FormData();
    formData.append("file", selectedFile.value);
    // Add your upload logic here (e.g., API call)
  }
};
</script>

<style lang="css" scoped>
.form-div {
  width: 100%;
  border: 1px solid olivedrab;
  margin-top: 2%;
  padding: 4px;
}
</style>
