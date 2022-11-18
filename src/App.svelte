<script lang="ts">
  import Grid from './Grid/Grid.svelte';  
  let cellSpacing = 1;
  let cellSize = 30;
</script>

<main>
  <div class="controls">
    <input placeholder="Spacing" type="number" min={1} bind:value={cellSpacing} />
    <input placeholder="Size" type="number" min={1} bind:value={cellSize} />
  </div>
  <Grid cellSpacing={cellSpacing} cellSize={cellSize}/>
</main>

<style>
  main {
    text-align: center;
    padding: 0;
    background-color: rgb(15, 27, 8);
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .controls {
    position: absolute;
    top: 100px;
    margin: 0 auto;
    left: 50%;
    padding: 30px;
    background: #fff9;
    backdrop-filter: blur(10px);
    border-radius: 20px;
  }
</style>
