<template>
  <div class="slidev-layout image-layout">
    <div class="top-bar" />
    <div class="header"><slot name="header" /></div>
    <div class="img-area"><slot /></div>
    <div class="footer"><slot name="footer" /></div>
  </div>
</template>

<style scoped>
.image-layout {
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
.img-area {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 0;
  overflow: hidden;
  padding: 0 2.2rem;
}
.img-area :deep(img) {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}
.img-area :deep(p) {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%; height: 100%;
  margin: 0;
}
.footer { flex-shrink: 0; padding: 0.4rem 2.2rem 1.6rem; }
</style>
