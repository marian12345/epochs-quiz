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
  throw new Error('epochs array is empty')
}

//
function getRandomEpoch(): Epoch {
  const index = Math.floor(Math.random() * epochs.length)
  return epochs[index]
}

const currentEpoch = ref<Epoch>(getRandomEpoch())

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
