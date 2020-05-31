<script>
  import Nav from "../components/Nav.svelte";
  export let segment;
</script>

<style>
  main {
    position: relative;
    background-color: white;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
</style>

<Nav {segment} />

<main class="relative">
  <slot />
</main>
