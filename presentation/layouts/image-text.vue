<template>
  <div class="slidev-layout image-text">
    <div class="top-bar" />
    <div class="header"><slot name="header" /></div>
    <div class="columns">
      <div class="img-side"><slot name="image" /></div>
      <div class="text-side"><slot name="text" /></div>
    </div>
  </div>
</template>

<style scoped>
.image-text {
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
  padding: 0.5rem 2.2rem 1rem;
}
.img-side {
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}
.img-side :deep(img) {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}
.img-side :deep(p) {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%; height: 100%;
  margin: 0;
}
.text-side {
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
}
</style>
