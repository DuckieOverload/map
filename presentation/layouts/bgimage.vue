<template>
  <div class="slidev-layout bgimage" :style="{ '--bg': bgUrl }">
    <div class="top-bar" />
    <div class="title"><slot name="title" /></div>
    <div class="card"><slot /></div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
const props = defineProps({
  image: { type: String, required: true },
})
const base = import.meta.env.BASE_URL.replace(/\/$/, '')
const bgUrl = computed(() => `url(${base}${props.image})`)
</script>

<style scoped>
.bgimage {
  width: 100%; height: 100%;
  padding: 0 !important;
  position: relative;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.bgimage::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: var(--bg);
  background-size: cover;
  background-position: center;
  z-index: 0;
}
.top-bar {
  width: 100%; height: 8px;
  background: #C69214;
  flex-shrink: 0;
  position: relative;
  z-index: 1;
}
.title {
  position: relative;
  z-index: 1;
  padding: 1.6rem 2.2rem 0.6rem;
}
.title :deep(h1) {
  color: white;
  text-shadow: 0 2px 8px rgba(0,0,0,0.5);
}
.card {
  position: relative;
  z-index: 1;
  background: rgba(255,255,255,0.88);
  border-radius: 12px;
  padding: 1.5rem 1.8rem;
  margin: 0 2.2rem;
  max-width: 55%;
}
.card :deep(p), .card :deep(li) {
  color: #222;
  font-size: 0.9rem;
}
.card :deep(ul) {
  font-size: 0.9rem;
  line-height: 2;
}
</style>
