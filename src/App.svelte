<script>
	export let name;
	import FibonacciCtrl from './FibonacciCtrl.svelte';
	import MagicSquare from './MagicSquare.svelte';
	
	const selections = [
		{text: "fibonacci", component: FibonacciCtrl},
		{text: "magic square", component: MagicSquare}
	]

	let selected = selections[1];
</script>

<style>
	h1 {
		color: purple;
	}
	#main {	
	    margin-left: 2%;
	}
</style>

<div id="main">
	<h1>Hello {name}!</h1>
	<select bind:value={selected}>
		{#each selections as selection}
			<option value={selection}>{selection.text}</option>
		{/each}
	</select>
	<svelte:component this={selected.component}/>
</div>