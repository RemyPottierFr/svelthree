<script>
  import * as THREE from "three";
  import { onMount } from "svelte";
  import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
  import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";

  export let modelName;
  export let modelSize;
  export let modelId;
  export let modelLight;
  export let modelAnimate;
  export let animationSpeed;
  export let axes;
  export let position;
  var processDone = false;

  const initDisplayer = node => {
    const sceneDimentions = node.parentNode.offsetWidth;
    console.log(sceneDimentions);
    // Setup scene
    let scene = new THREE.Scene();
    let camera = new THREE.PerspectiveCamera(30, 1, 1, 10000);
    camera.aspect = window.innerWidth / window.innerHeight;

    // Setup renderer
    let renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setSize(sceneDimentions, sceneDimentions);
    renderer.setClearColor(0xffffff, 0);

    // Setup ambiant light
    let light = new THREE.AmbientLight(0xffffff);
    light.intensity = modelLight;
    light.castShadow = false; // soft white light
    scene.add(light);

    if (axes) {
      //Add axes
      var axesHelper = new THREE.AxesHelper(
        modelSize === 0 ? 5 : modelSize === 1 ? 100 : modelSize === 2 ? 500 : 0
      );
      scene.add(axesHelper);
    }

    // Append to container
    const el = document.getElementById(modelId);
    el.appendChild(renderer.domElement);

    // Start loader of model
    let loader = new GLTFLoader();

    loader.load(
      `models/${modelName}`,
      function(gltf) {
        scene.add(gltf.scene);
        if (modelSize !== 0) {
          camera.position.set(20 * modelSize, 10 * modelSize, 15 * modelSize);
        } else {
          camera.position.set(20, 10, 15);
        }

        camera.lookAt(gltf.scene.position);

        if (position) {
          gltf.scene.position.set(position.x, position.y, position.z);
        }

        if (!modelAnimate) {
          const controls = new OrbitControls(camera, renderer.domElement);
        }
        let animate = function() {
          requestAnimationFrame(animate);
          if (modelAnimate) {
            gltf.scene.rotation.y +=
              animationSpeed === 1
                ? 0.003
                : animationSpeed === 2
                ? 0.01
                : animationSpeed === 3
                ? 0.1
                : 0;
          }
          if (position) {
            gltf.scene.position.set(position.x, position.y, position.z);
            // gltf.scene.matrix = inverse;
          }
          gltf.scene.matrixWorldNeedsUpdate = true;
          renderer.render(scene, camera);
          processDone = true;
        };

        animate();
      },
      undefined,
      // called when loading has errors
      function(error) {
        console.log(error);
      }
    );
  };
</script>

<div id={modelId} use:initDisplayer>
  {#if !processDone}
    <div class="w-full relative text-center">
      <img src="/images/copper-loader.gif" class="m-auto" alt="copper loader" />
    </div>
  {/if}
</div>
