<script>
  import { slide, fly, fade } from "svelte/transition";
  export let data = 7;
  export let isStack = true;
  export let size = 400;

  let colors = [
    "#E97451",
    "#FC80A5",
    "#C62D42",
    "#C9A0DC",
    "#76D7EA",
    "#FF8833",
    "#29AB87",
    "#AF593E",
    "#01786F",
    "#FFCBA4",
    "#FCD667",
    "#ED0A3F",
    "#FBE870",
    "#FED85D",
  ];

  let color = colors[Math.floor(Math.random() * colors.length)];
</script>

<!-- start html -->
<div
  class={isStack ? "stack" : "queue"}
  style={`background-color: ${color}`}
  id="block"
  transition:slide
  on:click={() => {}}
>
  <h1>{data}</h1>
</div>

<!-- end html -->
<style>
  #block {
    transition: all 0.3s cubic-bezier(0.165, 0.84, 0.44, 1);
  }

  .stack {
    width: 20vw;
    height: 5vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1.5px solid aliceblue;
  }

  .queue {
    width: 20vw;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1.5px solid aliceblue;
  }

  div:hover {
    filter: brightness(1.2);
    transform: scale(1.07);
  }

  h1 {
    text-align: center;
  }
</style>
