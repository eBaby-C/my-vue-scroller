<script setup>
import { ref } from 'vue';


const top = ref(null)

const toTop = () => {
  document.body.scrollTop = 0
  document.documentElement.scrollTop = 0
}

window.onscroll = () => {
  let res = document.body.scrollTop || document.documentElement.scrollTop
  if (res >= 800) top.value.style.display = 'block'
  else top.value.style.display = 'none'
}


</script>
<template>
  <div id="to_top" @click="toTop" ref="top"></div>
</template>
<style>
#to_top {
  width: 50px;
  height: 50px;
  border: 2px solid red;
  position: fixed;
  bottom: 100px;
  right: 20px;
  display: none;
  cursor: pointer;
}
</style>