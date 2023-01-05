<script setup>
import { defineProps, watchEffect, ref } from 'vue';


const props = defineProps({
  imgChoosed: String,
  image: Array
})

const imgChoosed = ref('')
const imgChoosedConfig = ref({})
const imgArr = ref([])
const div = ref(null)
const loadingMaxNum = 2
const observer = null

const loadData = () => {
  if (!imgChoosedConfig.value) return
  const { maxNum, minNum, type, imgPath } = imgChoosedConfig.value
  Array.from({ length: loadingMaxNum }, () => {
    const randomNum = Math.ceil(Math.random() * (maxNum - minNum)) + minNum
    const imgSrc = `../public/${imgPath}/${randomNum}.${type}`
    imgArr.value.push(imgSrc)
    // observe(div.value.children[imgArr.value.length - 1])

  })
  // 加载之后应该排布
  console.log(div.value.children[0]);

}
window.addEventListener('resize', () => {
  // colHeights = [500, 500, 500]
  // document.querySelectorAll('.card').forEach((card, index) => {
  // 	const cardHeight = card.clientHeight
  // 	const colIndex = (index + 1) % 3
  // 	colHeights[colIndex] += cardHeight
  // })
  setMasonryHeight()
})

//  scroller_view.style.height = `${Math.max(...colHeights) + 10}px`
const setMasonryHeight = () => console.log('object');

const observe = (cc) => {
	if (!observer) {
		observer = new IntersectionObserver((entries) => {
			if (entries.length === 1 && entries[0].isIntersecting) {
				// loadData()
				// observer.unobserve(entries[0].target)
			}
		})
	}
	observer.observe(div)
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
  <div id="img_container" ref="div">
    <template v-for="img in imgArr">
      <div class="card" >
        <img :src="img" alt="" class="show">
        <span>{{imgArr.indexOf(img)}}</span>
      </div>
    </template>
  </div>
</template>

<style>
:root {
  --card-width: 30vw;
  --divider-width: 2vw;
}

img {
  width: 100%;
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
  height: 100%;
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
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  flex-wrap: wrap;
  align-content: flex-start;
}
</style>

