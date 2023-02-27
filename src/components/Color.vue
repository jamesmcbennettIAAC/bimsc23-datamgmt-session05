<script setup>
import { ref } from "vue";

// Define props
const props = defineProps(['title'])

// Define emits
const emits = defineEmits(['updateColor'])

// Define variables with refs
var colorValue = ref(100)

// Define functions
function sendColorUpdate(){
  emits('updateColor', colorValue.value)
  
}


</script>

<template>
<div>
	<form class="definition-input">

      <label class="input-title" for="colorRange">{{ title }}</label>

      <input type="number" id="number" class="modern-range" v-model="colorValue" 
      v-on:input="sendColorUpdate">

	</form>
</div>


</template>

<style scoped>
.modern-range {
  appearance: none;
  -webkit-appearance: none;
  width: 100%;
  background: linear-gradient(90deg, lightgray, gray);
  height: 34px;
  width: 50%;
  float: right;
  border-radius: 15px;
  margin: 10px 0px;
  color: white;
  font-weight:bolder;
  font-size: 1rem;
}

</style>