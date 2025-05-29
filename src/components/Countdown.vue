<!-- src/components/Countdown.vue -->
<template>
  <v-container class="text-center">
    <h2>Nosso próximo aniversário de namoro é em:</h2>
    <v-row justify="center" class="mt-4">
      <v-col cols="auto" v-for="(value, label) in countdown" :key="label">
        <v-card color="pink">
          <v-card-text>
            <h3>{{ value }}</h3>
            <p>{{ label }}</p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const anniversaryDate = new Date('2025-09-26T00:00:00') // sua data de aniversário

const countdown = ref({ dias: 0, horas: 0, minutos: 0, segundos: 0 })

const updateCountdown = () => {
  const now = new Date()
  const diff = anniversaryDate - now

  if (diff <= 0) return

  countdown.value = {
    dias: Math.floor(diff / (1000 * 60 * 60 * 24)),
    horas: Math.floor((diff / (1000 * 60 * 60)) % 24),
    minutos: Math.floor((diff / 1000 / 60) % 60),
    segundos: Math.floor((diff / 1000) % 60),
  }
}

let interval
onMounted(() => {
  updateCountdown()
  interval = setInterval(updateCountdown, 1000)
})

onUnmounted(() => clearInterval(interval))
</script>
