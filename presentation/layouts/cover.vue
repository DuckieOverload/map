<template>
  <div class="cover">
    <div class="logos">
      <img src="/logo-a.png" />
      <img src="/logo-b.png" />
    </div>
    <div class="bar" />
    <div class="body"><slot /></div>
  </div>
</template>

<style scoped>
.cover {
  background: #182B49;
  width: 100%; height: 100%;
  display: flex; align-items: center;
  padding: 2.5rem 3rem; box-sizing: border-box;
  position: relative; gap: 1.5rem;
}
.logos {
  position: absolute; top: 1.5rem; right: 2rem;
  display: flex; gap: 0.75rem; align-items: center;
}
.logos img { height: 36px; object-fit: contain; }
.bar { width: 4px; height: 55%; flex-shrink: 0; background: #C69214; border-radius: 2px; }
.body { flex: 1; max-width: 70%; }
.body :deep(h1) {
  color: white; font-size: 2.2rem; font-weight: 300; line-height: 1.35;
  font-family: Merriweather, serif;
  margin: 0 0 0.5rem; border: none !important; padding: 0;
}
.body :deep(h2) {
  color: #C69214; font-size: 1.1rem; font-weight: 400;
  font-family: Merriweather, serif;
  margin: 0 0 0.9rem; border: none !important; padding: 0;
}
.body :deep(p) {
  color: rgba(255,255,255,0.6); font-size: 0.75rem; line-height: 1.7; margin: 0;
}
.body :deep(blockquote) {
  position: absolute;
  bottom: 1.5rem; left: 3rem; right: 3rem;
  background: rgba(0,0,0,0.2);
  border: none; border-left: none; border-radius: 6px;
  padding: 0.6rem 1rem;
  text-align: center;
  margin: 0;
}
.body :deep(blockquote p) {
  font-size: 0.65rem; color: rgba(255,255,255,0.6); margin: 0;
}
.body :deep(ul) {
  color: rgba(255,255,255,0.8); font-size: 0.8rem; line-height: 2.2;
  padding-left: 1.3rem; margin: 0.5rem 0 0;
}
</style>
