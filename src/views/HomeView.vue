<script setup lang="ts">
import { ref } from 'vue'
import { computed } from 'vue'
import CardComponent from '@/components/CardComponent.vue'
import ButtonComponent from '@/components/ButtonComponent.vue'
import jsonData from '../data/epochs.json'
import type { Epoch } from '../types/Epoch'

//Get epochs from json file
let epochs: Epoch[] = jsonData
if (!epochs.length) {
  throw new Error('Epochs array is empty')
}

//Get a random epoch from the array
function getRandomEpoch(): Epoch {
  const index = Math.floor(Math.random() * epochs.length)
  const randomEpoch = epochs[index]
  if (!randomEpoch) {
    throw new Error('Random epoch not found')
  }

  return randomEpoch
}

const currentEpoch = ref<Epoch>(getRandomEpoch())

//Get next Epoch after clicking the button
function nextEpoch() {
  let next = getRandomEpoch()

  currentEpoch.value = next
}
</script>

<template>
  <main>
    <CardComponent :epoch="currentEpoch" :key="currentEpoch.id" />

    <ButtonComponent @click="nextEpoch" />
  </main>
</template>

<style scoped></style>
