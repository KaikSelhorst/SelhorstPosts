# Three.js For Beginners

- [What's Three.js](#what-is-threejs)
- [Prerequisites](#prerequisites)
- [Create Renderer Scene Camera](#create-renderer-scene-camera)
- [Create SpotLight AmbientLight](#create-spotlight-ambientlight)
- [Create Object 3D External](#create-object-3d-external)
- [Animation Orbit Renderer mixerAnimation](#animation-orbit-renderer-mixeranimation)
- [All Code ⌨️](#all-code-⌨️)

### What's Three.js

Three.js is a powerful JavaScript library used for creating and displaying 3D graphics on the web. It provides a wide range of features for creating complex and interactive 3D scenes, including lighting, materials, textures, cameras, and more. Three.js is widely used by developers and designers to create stunning visualizations, games, and animations that can run directly in a web browser.

### Prerequisites

The only minimum requirement for a Node project is the installation of Node.js on your computer or server. Node.js is a runtime platform that allows you to run JavaScript applications on the server.

```bash
# Create Mininal Vanilla JavaScript Project starter
npm create vite@latest          # or yarn create vite

# Enter in project folder
cd <project-name>

# Install library Three.js
npm install three               # or yarn add three
```

I’m used this model in tutorial

[Fox](https://sketchfab.com/3d-models/fox-6144ebf03c914977921677a3e4ffffe2)

```js
// main.js

// Import library Three.js
import * as THREE from "three";
// Importing for control camera movement automatic
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
// For Load the 3D file  ex:fox.glb
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";
```

### Create `Renderer` `Scene` `Camera`

```js
// main.js

// Responsible for rendering the scene
const renderer = new THREE.WebGLRenderer();
// Superficially it activates the shadows in the scene
renderer.shadowMap.enabled = true;
// Size of the HTMLCanvasElement that is rendered on the screen
renderer.setSize(window.innerWidth, window.innerHeight);

// Create a scene component add change a background
const scene = new THREE.Scene();
scene.background = new THREE.Color("#D2FFE5");

// Create Perspective Camera for Scene
// Obs: you can use any variable name in CRATIO
// I'm using a CRATION that is Camera Ratio
const CRATIO = window.innerWidth / window.innerHeight;
const camera = new THREE.PerspectiveCamera(75, CRATIO, 0.1, 1000);
// Start Position camera
// Set method is (x,y,z) positions
camera.position.set(0, 2, 5);

// Create camera controls
const orbit = new OrbitControls(camera, renderer.domElement);
```

### Create `SpotLight` `AmbientLight`

```js
// main.js

// Creating the ambient lights, they are essential
// for creating the scenes

// Ambient light is emitted for the entire scene examples
// of ambient lights are: sunlight
const ambientLight = new THREE.AmbientLight(0x333333, 2.5);
scene.add(ambientLight);

// the spot light is a light similar to the
// directional light, its "only" difference is that
// along the way it increases its spot while in the
// directional light it is linear
const spotLight = new THREE.SpotLight(0xd2ffe5, 1);
scene.add(spotLight);
spotLight.position.set(70, 100, 100);
spotLight.castShadow = true; // enable for Light Emit Shadow
spotLight.angle = 0.2; // does not make the shadow pixelated
```

### Create `Object` `3D External`

```js
// main.js

// Create a first object in scene for scene,
// this object is a plane to reflect shadows
const planeGeometry = new THREE.PlaneGeometry(30, 30);
// MeshStandardMaterial is essential for casting shade and receiving
const planeMaterial = new THREE.MeshStandardMaterial({
  color: 0xd2ffe5,
  side: THREE.DoubleSide, // Enable two sides for the plane object
});
const plane = new THREE.Mesh(planeGeometry, planeMaterial);
// Add object in Scene
scene.add(plane);
plane.rotation.x = -0.5 * Math.PI;
plane.receiveShadow = true; // Enable for object receive Shadow

// URL path
const pathFox = new URL("./fox.glb", import.meta.url);
// GLTFLoader load GLTF and GLB
const loader = new GLTFLoader();
// For animation
let mixer, clips;

// Load Object Fox
// method load params is (path, loadCallback, progressCallback, errorCallback)
loader.load(pathFox.href, loadGLTF, null, (e) => console.log(e));

// Callback for load Object 3D
function loadGLTF(gltf) {
  const model = gltf.scene; // 3D Model
  clips = gltf.animations;
  mixer = new THREE.AnimationMixer(model); // Mixer for controlling animations
  scene.add(model);
  model.position.set(0, 4, 0);

  // Enable cast shadow  forin other objects
  // I used this code if it doesn't work use this
  // model.castShadow = true
  model.traverse((node) => (node.castShadow = true));

  // Start Animations
  clips.forEach((clip) => mixer.clipAction(clip).play());

  // there is usually a function called animate, this function
  // is responsible for animations, camera movements, etc.
  // I prefer to start it when the 3d model is loaded, but if
  // you want to put it at the end of the code, no problem.
  renderer.setAnimationLoop(animete);
}
```

### Animation `Orbit` `Renderer` `mixerAnimation`

```js
// main.js

// This animete function is responsible for animal scenes/objects
function animete() {
  // Update Camera Positions
  orbit.update();
  // render new Scene
  renderer.render(scene, camera);
  // animation speed time of object
  mixer.update(0.03);
}
```

### All Code ⌨️

```js
// main.js

import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";

const renderer = new THREE.WebGLRenderer();
renderer.shadowMap.enabled = true;
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.outputEncoding = THREE.sRGBEncoding;
document.querySelector("#app").appendChild(renderer.domElement);

const scene = new THREE.Scene();
scene.background = new THREE.Color("#D2FFE5");

const CRATIO = window.innerWidth / window.innerHeight;
const camera = new THREE.PerspectiveCamera(75, CRATIO, 0.1, 1000);

const orbit = new OrbitControls(camera, renderer.domElement);

camera.position.set(0, 2, 5);

const planeGeometry = new THREE.PlaneGeometry(30, 30);
const planeMaterial = new THREE.MeshStandardMaterial({
  color: 0xd2ffe5,
  side: THREE.DoubleSide,
});
const plane = new THREE.Mesh(planeGeometry, planeMaterial);
scene.add(plane);
plane.rotation.x = -0.5 * Math.PI;
plane.receiveShadow = true;

const ambientLight = new THREE.AmbientLight(0x333333, 2.5);
scene.add(ambientLight);

const spotLight = new THREE.SpotLight(0xd2ffe5, 1);
scene.add(spotLight);
spotLight.position.set(70, 100, 100);
spotLight.castShadow = true;
spotLight.angle = 0.2;

let mixer, clips;
function loadGLTF(gltf) {
  const model = gltf.scene;
  clips = gltf.animations;
  mixer = new THREE.AnimationMixer(model);
  scene.add(model);
  model.position.set(0, 4, 0);
  model.traverse((node) => (node.castShadow = true));

  clips.forEach((clip) => mixer.clipAction(clip).play());
  renderer.setAnimationLoop(animete);
}

const pathFox = new URL("./fox.glb", import.meta.url);
const loader = new GLTFLoader();

loader.load(pathFox.href, loadGLTF, null, (e) => console.log(e));

function animete() {
  orbit.update();
  renderer.render(scene, camera);
  mixer.update(0.03);
}
```

### Thanks for the learn this 🙂
