<script>
    import Fibonacci from './Fibonacci.svelte';

    let fibonacci_computing_spaces = [0,1,2];

</script>

<button on:click={e => fibonacci_computing_spaces = fibonacci_computing_spaces.concat([fibonacci_computing_spaces.length])}>
    Add new space
</button>

<button on:click={e => fibonacci_computing_spaces = fibonacci_computing_spaces.slice(0,fibonacci_computing_spaces.length-1)}>
    Remove new space
</button>

{#each fibonacci_computing_spaces as num}
    <Fibonacci>{num + 1}</Fibonacci>
{/each}