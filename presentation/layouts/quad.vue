<template>
  <div class="slidev-layout quad-layout">
    <div class="top-bar" />
    <div class="header"><slot name="header" /></div>
    <div class="grid">
      <div class="card"><slot name="tl" /></div>
      <div class="card"><slot name="tr" /></div>
      <div class="card"><slot name="bl" /></div>
      <div class="card"><slot name="br" /></div>
    </div>
  </div>
</template>

<style scoped>
.quad-layout {
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
.grid {
  flex: 1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  padding: 0.8rem 2.2rem 1.6rem;
  min-height: 0;
}
.card {
  background: #E8F5E9;
  border-radius: 10px;
  padding: 1.2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  overflow: hidden;
}
.card :deep(h3) {
  color: #2E7D32;
  font-size: 0.85rem;
  font-weight: 600;
  margin: 0.5rem 0 0.3rem;
  border: none;
  padding: 0;
}
.card :deep(p) {
  font-size: 0.78rem;
  color: #333;
  margin: 0;
}
.card :deep(svg) {
  flex-shrink: 0;
}
</style>
