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
    modelName="fox.gltf"
    modelSize={0}
    modelId="scene"
    modelLight={1} />
  <ModelDisplayer
    modelName="tire.gltf"
    modelSize={2}
    modelId="baseballglove2"
    modelLight={1} />
</div>
