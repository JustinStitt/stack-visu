<script>
  import { slide, fly, fade } from "svelte/transition";
  export let data = 7;
  export let isStack = true;
  export let size = 400;
  let color = Math.floor(Math.random() * 16777215).toString(16);

  const checkDarkColor = (_) => {
    if (color < 6000) {
      color = Math.floor(Math.random() * 16777215).toString(16);
    }
  };

  $: checkDarkColor(color);
</script>

<!-- start html -->
<div
  class={isStack ? "stack" : "queue"}
  style={`background-color: #${color}`}
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
    width: 300px;
    height: 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border: 1.5px solid aliceblue;
  }

  .queue {
    width: 40px;
    height: 300px;
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
