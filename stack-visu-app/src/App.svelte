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
    // blocks = [inp, ...blocks];
    blocks = [...blocks, inp];
  };

  const stackPop = () => {
    blocks = blocks.slice(0, blocks.length - 1);
  };

  const queuePop = () => {
    blocks = blocks.slice(1, blocks.length);
    console.log(blocks);
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

<main>
  <div class="blocks">
    {#if isStack}
      <h1>Stack Visualization!</h1>
    {/if}
    {#if !isStack}
      <h1>Queue Visualization!</h1>
    {/if}
    <div class={isStack ? "inner-stack" : "inner-queue"}>
      {#each blocks as block, i (block)}
        <Block data={block} {isStack} />
      {/each}
    </div>
  </div>
  <div class="controls">
    <button class="add-block" on:click={addBlock}> Add Block </button>
    <input
      type="text"
      bind:value={inp}
      style="width: 15%; text-align: center"
    />
    <button on:click={popBlock}> Remove Block </button>
    <button
      on:click={() => {
        isStack = !isStack;
      }}>Swap to Queue</button
    >
  </div>
</main>

<style>
  main {
    text-align: center;
    max-width: 240px;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: row;
    justify-content: center;
    overflow: hidden;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  .blocks {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: flex-end;
    background-color: #333;
    max-width: 500px;
  }

  .inner-stack {
    width: 100%;
    height: 325px;
    overflow-y: auto;
    border: 1px solid red;
    display: flex;
    flex-direction: column-reverse;
  }

  .inner-queue {
    width: 100%;
    height: 325px;
    overflow-y: auto;
    border: 1px solid red;
    display: flex;
    flex-direction: row;
  }
</style>
