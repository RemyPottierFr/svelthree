<script>
  import ModelDisplayer from "components/ModelDisplayer.svelte";
  import { onMount } from "svelte";

  let position = { x: -5, y: 0, z: 0 };
  const changeX = event => {
    console.log(event);
    // position.x = event.details
  };
</script>

<style>
  .section1 {
    background: #4a4e69af;
  }
</style>

<section class="section1" id="part2">
  <div class="flex flex-col md:flex-row items-center md:p-8 min-h-screen">
    <div class="flex flex-col w-full">
      <h1
        class="p-8 md:p-0 text-4xl md:text-5xl text-white font-bold font-mono
        header-title">
        Montrez vos créations en détails
      </h1>
      <p class="p-8 text-2xl text-white font-mono">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, nemo
        voluptates deserunt eum tempora laudantium iusto quibusdam, repudiandae
        sapiente impedit voluptatem odit velit quae, amet necessitatibus quo
        error neque ab.
      </p>
      <!-- <label for="rangeX">X:</label>
      <input id="rangeX" type="range" bind:value={position.x} />
      <label for="rangeX">Y:</label>
      <input id="rangeX" type="range" bind:value={position.y} />
      <label for="rangeX">Z:</label>
      <input id="rangeX" type="range" bind:value={position.z} /> -->
    </div>
    <div class="w-10/12 md:w-8/12 lg:4/12 -mt-16 md:mt-0">
      <ModelDisplayer
        modelName="fox.gltf"
        modelSize={1}
        modelId="fox"
        modelLight={1}
        position={false}
        modelAnimate
        animationSpeed={1}
        axes={false} />
    </div>
  </div>
</section>
