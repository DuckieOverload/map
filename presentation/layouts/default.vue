<template>
  <div class="slidev-layout sophon-default">
    <div class="top-bar" />
    <div class="body"><slot /></div>
  </div>
</template>

<style scoped>
.sophon-default {
  background: white;
  width: 100%; height: 100%;
  padding: 0 !important;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
.top-bar {
  width: 100%;
  height: 8px;
  background: #C69214;
  flex-shrink: 0;
}
.body {
  flex: 1;
  padding: 1.6rem 2.2rem 1.6rem;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}
</style>
