<script>
  import { fade, fly } from "svelte/transition";
  import Block from "./Components/Block.svelte";
  let blocks = [];

  let inp = 0;

  let isStack = true;

  const stackPush = () => {
    blocks = [...blocks, inp];
  };

  const queuePush = () => {
    if (blocks.length > 9) return; // too full
    // blocks = [inp, ...blocks];
    blocks = [...blocks, inp];
  };

  const stackPop = () => {
    blocks = blocks.slice(0, blocks.length - 1);
  };

  const queuePop = () => {
    blocks = blocks.slice(1, blocks.length);
  };

  const addBlock = () => {
    if (isStack) stackPush();
    else queuePush();
    inp += 1;
  };

  const popBlock = () => {
    if (isStack) stackPop();
    else queuePop();
  };
</script>

<main class="disable-dbl-tap-zoom">
  {#if isStack}
    <h1>Stack Visualization!</h1>
  {/if}
  {#if !isStack}
    <h1>Queue Visualization!</h1>
  {/if}
  <div class="blocks disable-dbl-tap-zoom">
    <div class={isStack ? "inner-stack" : "inner-queue"}>
      {#each blocks as block, i (block)}
        <Block data={block} {isStack} />
      {/each}
    </div>
  </div>
  <div class="controls">
    <button class="add-block disable-dbl-tap-zoom" on:click={addBlock}>
      Add Block
    </button>
    <!-- <input
      type="text"
      bind:value={inp}
      style="width: 15%; text-align: center"
    /> -->
    <button class="disable-dbl-tap-zoom" on:click={popBlock}>
      Remove Block
    </button>
    <button
      class="disable-dbl-tap-zoom"
      on:click={() => {
        isStack = !isStack;
      }}>Swap to {isStack ? "Queue" : "Stack"}</button
    >
  </div>
</main>

<style>
  main {
    text-align: center;
    max-width: 90vw;
    height: 85vh;
    padding: 0;
    margin-left: auto;
    margin-right: auto;
    /* margin-left: auto;
    margin-right: auto; */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    overflow: hidden;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
    background-color: #424242;
  }

  .blocks {
    max-width: 85vw;
    width: 90vw;
    max-height: 85vh;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: flex-end;
    background-color: #333;
    margin-bottom: 20px;
  }

  .inner-stack {
    width: 100%;
    height: 100%;
    max-height: 60vh;
    overflow-y: auto;
    /* border: 1px solid red; */
    display: flex;
    flex-direction: column-reverse;
    align-items: center;
  }
  .inner-queue {
    width: 100%;
    height: 100%;
    max-height: 60vh;
    overflow-y: hidden;
    overflow-x: auto;
    /* border: 1px solid red; */
    display: flex;
    flex-direction: row;
  }

  .disable-dbl-tap-zoom {
    touch-action: manipulation;
  }
</style>
