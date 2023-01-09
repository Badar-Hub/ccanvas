<template>
  <div class="row justify-between">
    <div class="image-slider-container">
      <div v-for="(img, i) in imageIds" :key="i" class="image-containers">
        <img class="image-slider" :src="img" @click="selectedImage = img" />
      </div>
    </div>
    <slot name="canvas" :data="selectedImage"></slot>
    <div class="class-info"></div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const selectedImage = ref("");
const imageIds = [
  "http://localhost:8080/01/01.jpg",
  "http://localhost:8080/01/02.jpg",
  "http://localhost:8080/01/03.jpg",
  "http://localhost:8080/01/04.jpg",
  "http://localhost:8080/01/05.jpg",
  "http://localhost:8080/01/06.jpg",
  "http://localhost:8080/01/07.jpg",
  "http://localhost:8080/01/08.jpg",
  "http://localhost:8080/01/09.jpg",
  "http://localhost:8080/01/10.jpg",
  "http://localhost:8080/01/11.jpg",
];
</script>

<style lang="scss">
.image-slider-container {
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
  max-height: calc(100vh - 100px);
  .image-slider {
    display: block;
    width: 200px;
    height: 150px;
  }
}
.class-info {
  width: 350px;
  background-color: #f2f2f2;
}
</style>
