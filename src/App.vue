<script setup>
import AutoScroller from './components/AutoScroller.vue';
import Header from './components/Header.vue';
import ToTop from './components/ToTop.vue';
import ImageContainer from './components/ImageContainer.vue';
import image from '../public/image.json';
import { ref } from 'vue';


const imgRef = ref('')

const imageInfo = e => imgRef.value = e.value



</script>

<template>
  <Header :image-option="image" @image-info="imageInfo" />
  <ImageContainer :img-choosed="imgRef" :image="image" />
  <ToTop />
  <AutoScroller />
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  color: #fff;
}

body {
  background-color: #000000;
}
</style>
