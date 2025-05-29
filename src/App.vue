<template>
  <v-app>
    <v-main style="background-color: #ffff5530!important;">
      <v-container >
        <div class="d-flex row align-center justify-center">
          <h1 class="text-center mt-4 love-title">Feliz Dia dos Namorados 💕</h1>
        </div>
        <BackGroundMusic />
        <LoveMessage />
        <Countdown />
        <PhotoGallery />
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import Countdown from "./components/Countdown.vue";
import PhotoGallery from "./components/PhotoGallery.vue";
import BackgroundMusic from "./components/BackGroundMusic.vue";
import LoveMessage from "./components/LoveMessage.vue";
</script>

<style>
@font-face {
  font-family: "Love Meadow";
  src: url(../src/assets/LoveMeadow-mL4V2.ttf) format("truetype");
}
.love-title {
  font-family: "Love Meadow", sans-serif;
  font-size: 3rem;
  color: #e91e63; /* rosa romântico */
  margin-bottom: 1rem;
  font-weight: lighter;
}
</style>
