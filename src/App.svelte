<script>
	export let name;
    import FibonacciCtrl from './FibonacciCtrl.svelte';
</script>

<style>
	h1 {
		color: purple;
	}
	#main {	
	    margin-left: 5%;
	}
</style>

<div id="main">
	<h1>Hello {name}!</h1>
	<FibonacciCtrl/>
</div>