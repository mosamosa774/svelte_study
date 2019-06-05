<script>
    import { memory } from './FibonacciMemory.js';

    let n = 0;
    $: result = compute_fibonacci(n);
    let changed_value = 1;

    function compute_fibonacci(n){
        let find = -1;
        memory.subscribe(memory => {
            if(n < memory.length){
                find = memory[n];
                return;
            }
            console.log(memory);
        });
        if(find != -1)
            return find;
        let res = compute_fibonacci(n-1) + compute_fibonacci(n-2);
        memory.update(n => n.concat([res]));
        return res;
    }

</script>

<style>
#fibonacci_div {
    width: 30%;
    border: 2px solid #000000;
	margin-left: 1%;
    margin-bottom: 1%;
}
</style>

<div id="fibonacci_div">
    <p> Fibonacci Computing Center <slot></slot></p>
    n = {n}<br/>
    result = {result} <br/>
    range = {changed_value} <br/><br/>

    <button on:click={e => n = n+changed_value}>
        +
    </button>

    <button on:click={e => n-changed_value >= 0 ? n = n-changed_value : 0}>
        -
    </button>
    <input type=range min=1 bind:value={changed_value}>
</div>