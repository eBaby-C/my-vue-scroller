<script setup>
import { ref } from 'vue';


const emit = defineEmits(['imageInfo'])
const props = defineProps({
  imageOption: Array,
})
// console.log(props.image)
const a = ref('')

const imageInfo = e => {
  a.value = e.target.textContent
  emit("imageInfo", a)
}
</script>
<template>
  <div id="v_navbar">
    <ul id="navbar_ul">
      <li v-for="i in imageOption" class="navbar_li" @click="imageInfo">
        <a>{{ i.optionName }}</a>
      </li>
    </ul>
  </div>
</template>
<style>
#v_navbar {
  position: fixed;
  width: 100%;
  border: 1px solid white;
  z-index: 1;
  text-align: center;
}

#navbar_ul {
  list-style-type: none;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  background-color: #000;
}

.navbar_li :hover {
  background-color: rgb(255, 123, 0);
  cursor: pointer;
  transition: all 300ms ease-out;
}

.navbar_li a {
  display: block;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  line-height: 25px;
}
</style>