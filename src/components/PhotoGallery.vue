<template>
  <v-container>
    <h2 class="text-center mb-4">Nossos Momentos 💑</h2>

    <v-carousel
      v-model="currentSlide"
      :height="carouselHeight"
      cycle
      interval="5000"
      hide-delimiters
      show-arrows="hover"
      class="fade-carousel"
    >
      <v-carousel-item v-for="(photo, i) in photos" :key="i">
        <v-img
          :src="photo"
          class="carousel-image"
          @click="openModal(photo)"
          style="cursor: zoom-in"
        />
      </v-carousel-item>
    </v-carousel>

    <!-- Modal fullscreen -->
    <v-dialog v-model="isModalOpen" fullscreen persistent>
      <v-card class="d-flex flex-column align-center justify-center" flat>
        <v-btn icon class="close-btn" @click="isModalOpen = false" color="pink">
          <v-icon color="white">mdi-close</v-icon>
        </v-btn>
        <v-img :src="selectedPhoto" class="fullscreen-img" />
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const photos = [
  "/fotos/nos1.jpg",
  "/fotos/nos2.jpg",
  "/fotos/nos3.jpg",
  "/fotos/nos4.jpg",
  "/fotos/nos5.jpg",
  "/fotos/nos6.jpg",
  "/fotos/nos7.jpg",
  "/fotos/nos8.jpg",
  "/fotos/nos9.jpg",
  "/fotos/nos10.jpg",
  "/fotos/nos11.jpg",
  "/fotos/nos12.jpg",
  "/fotos/nos13.jpg",
  "/fotos/nos14.jpg",
  "/fotos/nos15.jpg",
  "/fotos/nos16.jpg",
  "/fotos/nos17.jpg",
  "/fotos/nos18.jpg",
  "/fotos/nos19.jpg",
  "/fotos/nos20.jpg",
  "/fotos/nos21.jpg",
  "/fotos/nos22.jpg",
  "/fotos/nos23.jpg",
  "/fotos/nos24.jpg",
  "/fotos/nos25.jpg",
  "/fotos/nos26.jpg",
];

const currentSlide = ref(0);
const carouselHeight = ref("400");

const isModalOpen = ref(false);
const selectedPhoto = ref(null);

const openModal = (photo) => {
  selectedPhoto.value = photo;
  isModalOpen.value = true;
};

const updateHeight = () => {
  carouselHeight.value = window.innerWidth < 600 ? "250" : "400";
};

onMounted(() => {
  updateHeight();
  window.addEventListener("resize", updateHeight);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", updateHeight);
});
</script>

<style scoped>
.fade-carousel .v-window__container {
  transition: opacity 1s ease-in-out !important;
}

.fade-carousel .v-window-item {
  opacity: 0;
  transition: opacity 1s ease-in-out !important;
}

.fade-carousel .v-window-item.v-window-item--active {
  opacity: 1;
}

.carousel-image {
  height: 100%;
  width: 100%;
  object-fit: cover;
  object-position: center;
}

.fullscreen-img {
  width: 100%;
  height: 100vh;
  object-fit: contain;
  background-color: black;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  z-index: 10;
}
</style>
