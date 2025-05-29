<!-- src/components/BackgroundMusic.vue -->
<template>
  <div class="text-center my-4">
    <v-row align="center" justify="center" dense class="ga-2">
      <v-btn color="pink" icon @click="prevTrack">
        <v-icon color="white">mdi-skip-previous</v-icon>
      </v-btn>

      <v-btn color="pink" icon @click="togglePlayback">
        <v-icon color="white">{{
          isPlaying ? "mdi-pause-circle" : "mdi-play-circle"
        }}</v-icon>
      </v-btn>

      <v-btn color="pink" icon @click="nextTrack">
        <v-icon color="white">mdi-skip-next</v-icon>
      </v-btn>

      <v-col cols="12" sm="4" class="mt-3">
        <v-slider
          v-model="volume"
          min="0"
          max="1"
          step="0.01"
          thumb-label
          @update:modelValue="updateVolume"
          color="pink"
        />
      </v-col>
    </v-row>
    <p class="mt-2">
      Tocando agora: <strong>{{ currentTrackName }}</strong>
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted, watch, computed } from "vue";

const musicList = [
  { name: "The Only Exception - Paramore", file: "/musicas/musica1.mp3" },
  { name: "You & I - One Direction", file: "/musicas/musica2.mp3" },
  { name: "Always - blink-182", file: "/musicas/musica3.mp3" },
];

const currentTrackIndex = ref(0);
const isPlaying = ref(false);
const volume = ref(0.5);

const currentTrackName = computed(
  () => musicList[currentTrackIndex.value].name
);

let audio = null;

const loadTrack = () => {
  if (audio) {
    audio.pause();
    audio = null;
  }

  audio = new Audio(musicList[currentTrackIndex.value].file);
  audio.volume = volume.value;
  audio.play();
  isPlaying.value = true;

  // Trocar para próxima música automaticamente
  audio.addEventListener("ended", () => {
    nextTrack();
  });
};

const togglePlayback = () => {
  if (!audio) return;
  if (isPlaying.value) {
    audio.pause();
  } else {
    audio.play();
  }
  isPlaying.value = !isPlaying.value;
};

const nextTrack = () => {
  currentTrackIndex.value = (currentTrackIndex.value + 1) % musicList.length;
  loadTrack();
};

const prevTrack = () => {
  currentTrackIndex.value =
    (currentTrackIndex.value - 1 + musicList.length) % musicList.length;
  loadTrack();
};

const updateVolume = () => {
  if (audio) audio.volume = volume.value;
};

onMounted(() => {
  loadTrack();

  // Garantir autoplay com interação do usuário
  document.addEventListener(
    "click",
    () => {
      if (!isPlaying.value && audio) {
        audio.play();
        isPlaying.value = true;
      }
    },
    { once: true }
  );
});
</script>
