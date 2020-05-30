<script>
  import * as THREE from "three";
  import { onMount } from "svelte";
  import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";

  export let modelName;
  export let modelSize;
  export let modelId;
  export let modelLight;

  onMount(() => {
    // Setup scene
    let scene = new THREE.Scene();
    let camera = new THREE.PerspectiveCamera(
      30,
      window.innerWidth / window.innerHeight,
      1,
      10000
    );

    // Setup renderer
    let renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setClearColor(0xffffff, 0);

    // Setup ambiant light
    let light = new THREE.AmbientLight(0xffffff);
    light.intensity = modelLight;
    light.castShadow = false; // soft white light
    scene.add(light);

    //Add axes
    var axesHelper = new THREE.AxesHelper(
      modelSize === 0 ? 5 : modelSize === 1 ? 100 : modelSize === 2 ? 500 : 0
    );
    scene.add(axesHelper);

    // Append to container
    const el = document.getElementById(modelId);
    el.appendChild(renderer.domElement);

    // Render model
    function render() {
      renderer.render(scene, camera);
    }

    // Start loader of model
    let loader = new GLTFLoader();

    loader.load(
      `models/${modelName}`,
      function(gltf) {
        scene.add(gltf.scene);
        if (modelSize === 0) {
          camera.position.set(20, 10, 15);
        } else if (modelSize === 1) {
          camera.position.set(100, 70, 70);
        } else if (modelSize === 2) {
          camera.position.set(600, 400, 400);
        }

        camera.lookAt(gltf.scene.position);
        let animate = function() {
          requestAnimationFrame(animate);
          gltf.scene.rotation.y += 0.003;
          renderer.render(scene, camera);
        };

        animate();
      },
      undefined,
      // called when loading has errors
      function(error) {
        console.log(error);
      }
    );
  });
</script>

<style>
  #three {
    width: 100%;
    height: 100vh;
  }
</style>

<div id={modelId} />
