<script>
  import ModelDisplayer from "components/ModelDisplayer.svelte";
  import { fly } from "svelte/transition";
  import { onMount } from "svelte";

  let header = false;

  onMount(() => {
    header = true;
  });
</script>

<style>
  .header {
    background: #4a4e69;
  }
</style>

{#if header}
  <div class="header" id="part1">
    <div
      class="flex flex-col md:flex-row items-center md:p-8 md:items-start
      min-h-screen"
      transition:fly={{ y: -200, duration: 2000 }}>
      <div class="w-10/12 md:w-7/12 lg:4/12 md:-mt-16">
        <ModelDisplayer
          modelName="scene_baseballglove_0.glb"
          modelSize={40}
          modelId="baseballglove0"
          modelLight={3}
          modelAnimate
          animationSpeed={1}
          axes={false} />
      </div>
      <div class="flex flex-col md:-ml-8">
        <h1
          class="p-8 md:p-0 text-4xl md:text-5xl text-white font-bold font-mono
          header-title">
          Afficher vos créations 3D simplement
        </h1>
        <p class="p-8 text-2xl text-white font-mono">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi,
          nemo voluptates deserunt eum tempora laudantium iusto quibusdam,
          repudiandae sapiente impedit voluptatem odit velit quae, amet
          necessitatibus quo error neque ab.
        </p>
      </div>
    </div>
  </div>
{/if}
