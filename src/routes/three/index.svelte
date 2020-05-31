<script>
  import ModelDisplayer from "components/ModelDisplayer.svelte";
  import { fly } from "svelte/transition";
  import { onMount } from "svelte";

  let header = false;

  onMount(() => {
    header = true;
  });
</script>

<div class="flex flex-col bg-blue-900">
  {#if header}
    <div
      class="flex flex-col items-center p-8 h-screen"
      transition:fly={{ y: -200, duration: 2000 }}>
      <ModelDisplayer
        modelName="scene_baseballglove_0.glb"
        modelSize={2}
        modelId="baseballglove0"
        modelLight={3}
        sceneWidth={500}
        sceneHeight={400}
        modelAnimate
        animationSpeed={1}
        axes={false} />
      <div class="flex flex-col">
        <p class="text-2xl font-bold">svelthree</p>
      </div>
    </div>
  {/if}
</div>
