<template>
  <CCanvasLayout :selected-image-id="{ image }">
    <template #canvas="{ data }">
      <CCanvas :image-url="data" />
    </template>
  </CCanvasLayout>
</template>

<script setup>
import CCanvas from "./components/CCanvas.vue";
import CCanvasLayout from "./components/CCanvasLayout.vue";
</script>

<style lang="scss"></style>
