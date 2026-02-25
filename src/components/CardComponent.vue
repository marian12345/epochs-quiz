<script setup lang="ts">
import { ref } from 'vue'
import type { Epoch } from '../types/Epoch'
const props = defineProps<{
  epoch: Epoch
}>()
const currEpoch: Epoch = props.epoch

const isFlipped = ref(false)
function toggleFlip() {
  isFlipped.value = !isFlipped.value
}
</script>

<template>
  <div class="card-container">
    <div class="flip-card" @click="toggleFlip">
      <div class="flip-card-inner" :class="{ flipped: isFlipped }">
        <div class="flip-card-front">
          <p class="title">{{ currEpoch.name }}</p>
          <p>Click Me</p>
        </div>
        <div class="flip-card-back">
          <p class="title">{{ currEpoch.timePeriod }}</p>
          <p>Click Me</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.flip-card {
  background-color: transparent;
  width: 190px;
  height: 254px;
  perspective: 1000px;
  font-family: sans-serif;
  cursor: pointer;
}

.title {
  font-size: 1.5em;
  font-weight: 900;
  text-align: center;
  margin: 0;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card-inner.flipped {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  box-shadow: 0 8px 14px 0 rgba(0, 0, 0, 0.2);
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  border: 1px solid coral;
  border-radius: 1rem;
}

.flip-card-front {
  background: var(--color-background-mute);
  color: coral;
}

.flip-card-back {
  background: var(--color-background-mute);
  color: white;
  transform: rotateY(180deg);
}
</style>
