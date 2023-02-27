<script setup>
import { ref } from "vue";

// Define props
const props = defineProps(['title'])

// Define emits
const emits = defineEmits(['updateColor'])

// Define variables with refs
var color = ref('#2bff00')

// Define functions
function sendColorUpdate(){
  emits('updateColor', color.value)
}


</script>

<template>
<div>
	<form class="definition-input">

      <label class="input-title-color">{{ title }}: </label> 
      <input type="color" id="torusColor" name="torusColor" v-model="color" v-on:change="sendColorUpdate">
     
	</form>
</div>


</template>

<style>
.input-title-color {
  border-width: 0px;
  border-style: hidden;
  font: lexend;
  font-size: 1.6rem;
  font-weight: bold;
}


#torusColor {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  width: 100%;
  height: 50px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  padding-top: 5px
}
#torusColor::-webkit-color-swatch {
  border-radius: 15px;
  border: none;
}
#torusColor::-moz-color-swatch {
  border-radius: 15px;
  border: none;
}
</style>