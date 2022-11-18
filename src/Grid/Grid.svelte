<script lang="ts">
  import { Colord, colord } from "colord";

  function randColor(): string {
    return `#${Math.floor(Math.random() * 0xffffff)
      .toString(16)
      .padStart(6, "0")}`;
  }

  class Counter {
    count = 50;
    ended = false;
    decrement() {
      this.count -= 1;
      this.ended = this.count === 0;
    }
    reset() {
      this.count = 100;
      this.ended = false;
    }
  }

  class Cell {
    animating: boolean = false;
    original: string = randColor();

    color: Colord = colord(this.original);
    counter: Counter = new Counter();

    lighten() {
      const isWhite = this.color.toHex() === "#ffffff";
      this.color = isWhite ? colord("#000000") : colord("#ffffff");
      this.counter.decrement();
      return true;
    }

    reset() {
      this.color = colord(this.original);
      this.counter.reset();
      this.animating = false;
      return false;
    }

    animate() {
      this.animating = true;
      if (this.counter.ended) {
        return this.reset();
      }
      return this.lighten();
    }
    endAnimation() {
      this.animating = true;
      this.reset();
    }
  }

  export let cellSize: number;
  export let cellCount: number;

  function makeRows(count: number) {
    return Array.from({ length: count }, () => Array.from({ length: count }, () => new Cell()));
  }

  function run(cell: Cell) {
    window.requestAnimationFrame(() => {
      if (cell.animate()) {
        run(cell);
      }
      rows = rows;
    });
  }

  function initAnimation(cell: Cell) {
    if (!cell.animating) {
      run(cell);
    }
  }

  function makeGridStyle(count: number) {
    return [
      `grid-template-columns: repeat(${count}, 0fr)`,
      `grid-template-rows: repeat(${count}, 0fr)`,
    ].join(";");
  }

  $: rows = makeRows(cellCount);
  $: gridStyle = makeGridStyle(cellCount);
  $: cellStyle = `width: ${cellSize}px; height: ${cellSize}px;`;
</script>

<div class="grid" style={gridStyle}>
  {#each rows as row}
    {#each row as col}
      <div
        style={`${cellStyle} background: ${col.color.toHex()}`}
        class="cell"
        on:mouseenter={() => initAnimation(col)}
      />
    {/each}
  {/each}
</div>

<style>
  .grid {
    display: inline-grid;
    row-gap: 2px;
    column-gap: 2px;
    margin: 0 auto;
  }
  .cell {
    width: 20px;
    height: 20px;
    border-radius: 4px;
  }
</style>
