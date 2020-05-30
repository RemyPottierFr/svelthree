<script>
  import ModelDisplayer from "components/ModelDisplayer.svelte";
</script>

<style>
  .bg-black {
    background: linear-gradient(#e66465, #9198e5);
  }
</style>

<div class="bg-black">
  <ModelDisplayer
    modelName="scene.gltf"
    modelSize={0}
    modelId="scene"
    modelLight={1} />
  <ModelDisplayer
    modelName="scene_baseballglove_2.glb"
    modelSize={2}
    modelId="baseballglove2"
    modelLight={3} />
  <ModelDisplayer
    modelName="scene_baseballglove_0.glb"
    modelSize={2}
    modelId="baseballglove2"
    modelLight={3} />
</div>
