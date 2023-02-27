<template>
  <div id="viewport" class="flex flex-col p-4">
    <div id="threejs-container" class="py-5"></div>
  </div>
</template>

<script setup>
// Imports;
import { onMounted, onUpdated } from "vue";
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";

// Property coming from parent component
const props = defineProps(['radius', 'tube', 'tubeSegments', 'radialSegments', 'meshBoolean', 'Red', 'Blue', 'Green']);


// Three js objects
let renderer, camera, scene, controls, geometry;

let width = 1000;
let heigh = 700;

function init() {
  // rendeder
  renderer = new THREE.WebGLRenderer();
  renderer.setSize(width, heigh);
  renderer.setPixelRatio(window.devicePixelRatio);
  document.getElementById("threejs-container").appendChild(renderer.domElement);

  // camera
  camera = new THREE.PerspectiveCamera(25, width / heigh, 0.1, 1000);
  camera.position.set(10, 50, 70);

  // scene
  scene = new THREE.Scene();
  scene.background = new THREE.Color("#000000");
  


  // orbit controls
  controls = new OrbitControls(camera, renderer.domElement);

  // add fun shape
  createTorusKnot(10, 3, 100, 16);
  animate();
}

// for controls update
function animate() {
  
  requestAnimationFrame(animate);
  controls.update();
  renderer.render(scene, camera);


}

function createTorusKnot(radius, tube, tubeSegments, radialSegments) {
  geometry = new THREE.TorusKnotGeometry( radius, tube, tubeSegments, radialSegments );
  const material = new THREE.MeshStandardMaterial({color: new THREE.Color(props.Red, props.Blue, props.Green), wireframe: props.meshBoolean});
  const torusKnot = new THREE.Mesh(geometry, material);
  scene.add(torusKnot);

  
      // Add lights to the scene
      const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
    scene.add(ambientLight);

    const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
    directionalLight.position.set(1, 1, 1);
    scene.add(directionalLight);
}

function onSliderChange() {
  scene.clear();
  //createBox(props.size1, props.size2, props.size3);
  createTorusKnot(props.radius, props.tube, props.tubeSegments, props.radialSegments);
}


// This function runs at the beginning of the component lifecycle.
// More about Vue lifecycles: https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram
onMounted(() => {
  init();
  animate();
});

// This function runs when DOM updates.
onUpdated(() => {
  // text content should be the same as current `count.value`
  onSliderChange();

});

</script>

<!-- <style scoped>
#viewport {
  border-style: dashed;
  border-color: #d2dfe8;
  border-width: 4px;
  border-radius: 10px;
  margin: 12px;
  height: calc(100vh - 105px);
  width: 600px;
  min-width: 200px;
  position: inherit;
}
</style> -->