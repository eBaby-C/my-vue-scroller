<script setup>
import { defineProps, watchEffect, ref } from 'vue';


const props = defineProps({
  imgChoosed: String,
  image: Array
})

const imgChoosed = ref('')
const imgChoosedConfig = ref({})
const imgArr = ref([])
const loadingMaxNum = 5

const loadData = () => {
  if (!imgChoosedConfig.value) return
  const { maxNum, minNum, type, imgPath } = imgChoosedConfig.value
  Array.from({length: loadingMaxNum}, () => {
    const randomNum = Math.ceil(Math.random() * (maxNum - minNum)) + minNum
    const imgSrc = `../public/${imgPath}/${randomNum}.${type}`
    imgArr.value.push(imgSrc)
  })
}

watchEffect(
  () => {
    imgArr.value = []
    const { image } = props
    imgChoosed.value = props.imgChoosed
    imgChoosedConfig.value = image.filter(i => i.optionName == imgChoosed.value)[0]
    setTimeout(loadData)
  }
)

</script>

<template>
  <div id="img_container">
    <template v-for="img in imgArr">
      <div class="card">
        <img :src="img" alt="" class="show">
      </div>
    </template>
  </div>

  <button @click="loadData" style="position: fixed; top: 30vh;left: 30vw;z-index: 1;">
    123
  </button>
</template>

<style>

:root {
	--card-width: 30vw;
	--divider-width: 2vw;
}

img {
  max-height: 70vh;
}

.show {
  animation-name: slideIn;
  animation-duration: 1s;
  animation-fill-mode: both;
  animation-timing-function: ease-in-out;
}

.card {
	width: 30vw;
	padding-bottom: 30px;
	position: relative;
}

.card:nth-of-type(3n + 1) {
	order: 1;
}
.card:nth-of-type(3n + 2) {
	order: 2;
}
.card:nth-of-type(3n + 3) {
	order: 3;
}

@keyframes slideIn {
  from {
    filter: opacity(0);
    transform: translateY(100px);
  }

  to {
    filter: opacity(1);
    transform: translateY(0);
  }
}

#img_container {
  padding-top: 60px;
	width: calc(var(--card-width) * 3 + var(--divider-width) * 2);
	min-height: 100vh;
	margin: 0 auto;
  display: flex;
	flex-direction: column;
	flex-wrap: wrap;
	align-content: flex-start;
}

</style>

