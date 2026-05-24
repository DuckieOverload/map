<template>
  <div class="slidev-layout two-cols">
    <div class="top-bar" />
    <div class="header"><slot name="header" /></div>
    <div class="columns">
      <div :class="['col', leftClass]"><slot name="left" /></div>
      <div :class="['col', rightClass]"><slot name="right" /></div>
    </div>
    <div class="footer"><slot name="footer" /></div>
  </div>
</template>

<script setup>
defineProps({
  leftClass: { type: String, default: '' },
  rightClass: { type: String, default: '' },
})
</script>

<style scoped>
.two-cols {
  background: white;
  width: 100%; height: 100%;
  padding: 0 !important;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.top-bar {
  width: 100%; height: 8px;
  background: #C69214;
  flex-shrink: 0;
}
.header { flex-shrink: 0; padding: 1.6rem 2.2rem 0; }
.columns {
  flex: 1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  min-height: 0;
  padding: 0.5rem 2.2rem 0;
}
.col {
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.footer { flex-shrink: 0; padding: 0 2.2rem 1.6rem; }
</style>
