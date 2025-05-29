<!-- src/components/LoveMessage.vue -->
<template>
  <v-container class="text-center my-10">
    <h2 class="text-h5 text-md-h4 font-weight-medium typewriter-text">
      {{ displayedText }}
    </h2>
  </v-container>
</template>

<script setup>
import { ref, onMounted } from "vue";

const messages = [
  "Você é meu lugar favorito no mundo. 💕",
  "Cada dia ao seu lado é um capítulo lindo da nossa história. 📖",
  "Te amo mais do que ontem, mas menos do que amanhã. 💘",
  "Seu sorriso é meu pôr do sol favorito. 🌅",
  "Com você, tudo faz sentido. 💫",
];

const displayedText = ref("");
let messageIndex = 0;
let charIndex = 0;
let typing = true;

const typeMessage = () => {
  const currentMessage = messages[messageIndex];

  if (typing) {
    if (charIndex < currentMessage.length) {
      displayedText.value += currentMessage.charAt(charIndex);
      charIndex++;
      setTimeout(typeMessage, 50);
    } else {
      typing = false;
      setTimeout(typeMessage, 2000); // Espera após digitar
    }
  } else {
    if (charIndex > 0) {
      displayedText.value = displayedText.value.slice(0, -1);
      charIndex--;
      setTimeout(typeMessage, 25);
    } else {
      typing = true;
      messageIndex = (messageIndex + 1) % messages.length;
      setTimeout(typeMessage, 400);
    }
  }
};

onMounted(() => {
  typeMessage();
});
</script>

<style scoped>
.typewriter-text {
  white-space: pre-wrap;
  font-family: "Courier New", monospace;
  border-right: 2px solid pink;
  animation: blink 0.75s step-end infinite;
  min-height: 100px;
  padding-bottom: 1rem;
}

@keyframes blink {
  from,
  to {
    border-color: transparent;
  }
  50% {
    border-color: pink;
  }
}
</style>
