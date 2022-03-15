<script>
	import { fade, fly} from 'svelte/transition';
	import Block from './Components/Block.svelte'
	let blocks = [];
	let inp = 0;
	const addBlock = () => {
		blocks = [...blocks, inp]
	}

	const popBlock = () => {
		blocks = blocks.slice(0, blocks.length-1);
	}
</script>

<main>
	<div class='blocks'>
		<h1>Stack Visualization!</h1>
		<div class='inner'>
			{#each blocks as block}
			<Block data={block}/>
			{/each}
		</div>
		<h4 style='color: aliceblue;'>
			Last Update: 3/15/2022 15:59 PST
		</h4>
	</div>
	<div class='controls'>
		<button class='add-block' on:click={addBlock}>
			Add Block
		</button>
		<input type="text" bind:value={inp} style='width: 15%; text-align: center'>
		<button  on:click={popBlock}>
			Remove Block
		</button>
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
	}
	
	.inner {
		width: 100%;
		height: 325px;
		overflow-y: auto;
		border: 1px solid red;
		display: flex;
		flex-direction: column-reverse;
	}


</style>