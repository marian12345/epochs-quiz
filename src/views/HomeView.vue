<script setup lang="ts">
import { computed } from 'vue'
import CardComponent from '@/components/CardComponent.vue'
import jsonData from '../data/epochs.json'
import type { Epoch } from '../types/Epoch'

let epochs: Epoch[] = jsonData
if (!epochs.length) {
  throw new Error('epochs array is empty')
}

const randomEpoch = computed<Epoch>(() => {
  const index = Math.floor(Math.random() * epochs.length)
  return epochs[index]
})
</script>

<template>
  <main><CardComponent :epoch="randomEpoch" /></main>
</template>
