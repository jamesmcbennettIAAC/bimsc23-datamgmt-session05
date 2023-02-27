<!-- // Script is in some way equivalent to script.js. This is place
to define variables, methods and imports of other Vue compoennts. -->
<script setup>
// Import other Vue components in order to add them to a template.
import SliderInput from "./components/SliderInput.vue";
import ToggleInput from "./components/ToggleInput.vue";
import GeometryView from "./components/GeometryView.vue";
import Color from "./components/Color.vue";

// Imports from packages

// Understanding ref article: https://blog.logrocket.com/understanding-vue-refs/#:~:text=Ref%20s%20are%20Vue.,element%20in%20your%20Vue%20instance.
// When ref attribute is added to element, this element then can be referenced
// in template. It is sort of templatecement of getElementById (but better)
import { ref } from "vue";

// Define variables and constants

var slider1 = ref(10);
var slider2 = ref(3);
var slider3 = ref(200);
var slider4 = ref(16);

var runToggle = ref(false);

var numinput1 = ref(100);
var numinput2 = ref(255);
var numinput3 = ref(255);

function updateValue(newValue, parameterName) {
  if (parameterName === "Radius") {
    slider1.value = newValue;
    console.log(newValue)
  }
  if (parameterName === "Tube") {
    slider2.value = newValue;
  }
  if (parameterName === "TubeSegments") {
    slider3.value = newValue;
  }
  if (parameterName === "RadialSegments") {
    slider4.value = newValue;
  }
}




function updateToggle(newValue) {
  runToggle.value = newValue;
  console.log(newValue)
}





function updateColor(newValue, parameterName) {
  if (parameterName === "Red") {
    numinput1 = newValue;
    console.log(newValue)
  }
  if (parameterName === "Blue") {
    numinput2 = newValue;
  }
  if (parameterName === "Green") {
    numinput3 = newValue;
  }
}


</script>

<!-- Template is a HTML-based syntax that allows you to bind the rendered DOM elements
with data, objects, functions etc. -->
<template>
  <div id="top-bar">
    <div id="title-container">
      <img class="logo-image" alt="Iaac logo" src="./assets/iaac-white.png" />
      <h2>Digital Tools for Cloud-based Data Management</h2>
    </div>
  </div>

  <div id="content">
    <!-- First example -> button -->
    <!-- <button @click="increment">Add one more</button>
    <p>Count is: {{  count }}</p> -->
    <div class="titlebar">
      <!-- Vue component injected into App.vue component template.
      That makes it App.vue a parent and SliderInput.vue a child. -->
      <SliderInput title="Radius"
        v-bind:min="1" v-bind:max="20" v-bind:step="1"
        v-on:updateValue="updateValue"/>

        <SliderInput title="Tube"
        v-bind:min="1" v-bind:max="5" v-bind:step="1"
        v-on:updateValue="updateValue"/>

        <SliderInput title="TubeSegments"
        v-bind:min="1" v-bind:max="200" v-bind:step="1"
        v-on:updateValue="updateValue"/>

        <SliderInput title="RadialSegments"
        v-bind:min="1" v-bind:max="100" v-bind:step="1"
        v-on:updateValue="updateValue"/>
        



        <ToggleInput title="Wireframe" 
        v-on:updateValue="updateToggle">
        </ToggleInput>





        <Color title="Red" 
        v-on:updateValue="updateColor">
        </Color>

        <Color title="Blue"  
        v-on:updateValue="updateColor">
        </Color>

        <Color title="Green"
        v-on:updateValue="updateColor">
        </Color>

      <!--<h2>Value received in App.vue: {{ slider1 }}</h2>
      <h2>Value received in App.vue: {{ runToggle }}</h2>-->
    </div>

    <div id="content">
      <GeometryView :radius="slider1" :tube="slider2" :tubeSegments="slider3" :radialSegments="slider4" :meshBoolean="runToggle" :Red="numinput1" :Blue="numinput2" :Green="numinput3"/>

      <!-- uncomment to add another geometryview -->
      <!-- <GeometryView :size="firstSlider"/> -->
    </div>
  </div>
</template>

<!-- Style is for CSS styling -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
}

#top-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  /*background-color: rgb(0, 0, 0);*/
}

#title-container {
  display: flex;
  align-items: center;
  color: white;
  margin-right: 1.5rem;
}

#content {
  display: flex;
}

.logo-image {
  height: 3.25rem;
  padding: 0.5rem;
}
body {
  background: black;
}
h2 {
  font-size: 1.125rem;
  font-weight: 600;
  letter-spacing: -0.05em;
  font-size: 1.125rem;
  font-weight: 600;
  letter-spacing: 0.01em;
}
</style>
