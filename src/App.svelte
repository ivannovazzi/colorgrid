<script lang="ts">
  import Grid from './Grid/Grid.svelte';  
  let cellCount = 10;
  let cellSize = 10;
</script>

<main>
  <input placeholder="Count" type="number" min={1} bind:value={cellCount} />
  <input placeholder="Size" type="number" min={1} bind:value={cellSize} />
  <br/>
  <Grid cellCount={cellCount} cellSize={cellSize}/>
</main>

<style>
  main {
    text-align: center;
    padding: 0;
    background-color: rgb(15, 27, 8);
    height: 100%;
  }
</style>
