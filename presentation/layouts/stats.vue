<template>
  <div class="stats-layout">
    <div class="top-bar" />
    <div class="header"><slot name="header" /></div>
    <div class="cards"><slot /></div>
    <div class="footer"><slot name="footer" /></div>
  </div>
</template>

<style scoped>
.stats-layout {
  background: #182B49;
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
.header :deep(h1) {
  color: white; font-size: 1.8rem; font-weight: 700;
  font-family: Merriweather, serif;
  margin: 0 0 0.4rem; border-bottom: 3px solid #C69214;
  padding-bottom: 0.4rem;
}
.cards {
  flex: 1;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  min-height: 0;
  align-items: center;
  padding: 0 2.2rem;
}
.cards :deep(.stat-card) {
  background: #1E3A5F;
  border-radius: 8px;
  padding: 1.2rem;
  text-align: center;
}
.cards :deep(.stat-num) {
  font-size: 2.8rem;
  font-weight: 700;
  color: white;
  line-height: 1;
}
.cards :deep(.stat-label) {
  font-size: 0.65rem;
  color: rgba(255,255,255,0.6);
  margin-top: 0.3rem;
}
.cards :deep(.stat-sub) {
  font-size: 0.8rem;
  color: #C69214;
  font-weight: 500;
  margin-top: 0.5rem;
}
.footer { flex-shrink: 0; padding: 0.8rem 2.2rem 1.6rem; }
.footer :deep(p) {
  color: white; font-size: 0.85rem; text-align: center; margin: 0 0 0.3rem;
}
.footer :deep(small), .footer :deep(.caption) {
  display: block; text-align: center;
  background: #C69214; border-radius: 4px;
  padding: 0.2rem 0.8rem; font-size: 0.6rem; color: #182B49;
  width: fit-content; margin: 0.4rem auto 0;
}
</style>
