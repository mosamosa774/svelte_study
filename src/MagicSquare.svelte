<script>
    let box = [
        0,0,0,
        0,0,0,
        0,0,0
    ];

    let useable_values = [1,2,3,4,5,6,7,8,9];
    let generating_complete_magic_square = false;
    let is_animation = false;
    let result;

    /*function next(index,copied_values){
        let promise = new Promise(function(resolve, reject) {
            setTimeout(function() {
                resolve(investigate(index+1,copied_values));
            },100)
        });
        return promise;
    }*/

    function investigate(index,useable_values){
        if(index == 9){
            return generating_complete_magic_square ? checkCompleteMagicSquare() : checkMagicSquare();
        }
        
        for(let i in useable_values){
            let copied_values = useable_values.slice(0);
            box[index] = copied_values[i];
            copied_values.splice(copied_values.indexOf(box[index]),1);
            let res = investigate(index+1,copied_values);       
            /*if(is_animation == true){
                res = await next(index,copied_values);
            }*/
            if(res == true){
                return true;
            }
        }
        return false;
    }

    function checkMagicSquare(){
        return (box[0] + box[1] + box[2] == 15) &&
            (box[3] + box[4] + box[5] == 15) &&
            (box[6] + box[7] + box[8] == 15) &&
            (box[0] + box[3] + box[6] == 15) &&
            (box[1] + box[4] + box[7] == 15) &&
            (box[2] + box[5] + box[8] == 15);
    };

    function checkCompleteMagicSquare(){
        return (box[0] + box[1] + box[2] == 15) &&
            (box[3] + box[4] + box[5] == 15) &&
            (box[6] + box[7] + box[8] == 15) &&
            (box[0] + box[3] + box[6] == 15) &&
            (box[1] + box[4] + box[7] == 15) &&
            (box[2] + box[5] + box[8] == 15) &&
            (box[0] + box[4] + box[8] == 15) &&
            (box[2] + box[4] + box[6] == 15);
    };

    function initialize(){
        result = "dealing...";
        box = [
            0,0,0,
            0,0,0,
            0,0,0
        ];
        box[0] = Math.floor( Math.random() * 9) + 1;
        let copied_values = useable_values.slice(0);
        copied_values.splice(copied_values.indexOf(box[0]),1);
        investigate(1,copied_values) ? result = "success!" : result = "failed...";
    }

    computed: {
        initialize();
    }
</script>

<style>
.container {
  width: 50%;
  height: 50vh;
  border: 2px solid #000000;
}

.item {
  display: inline-block;
  width: 30%;
  height: 30%;
  margin-left: 2%;
  margin-top: 1vh;
  background-color: rgb(124, 255, 255);
  border: 1px solid #000000;
  font-size: 300%;
  text-align: center; 
}
</style>

<div class="container">
    {#each box as value}
        <div class="item">{value}</div>
    {/each}
</div>
<br>
Computing Result: {result}
<br>
<input type="checkbox" bind:value={is_animation}/>
Animation
<input type="checkbox" bind:value={generating_complete_magic_square}/>
Complete Magic Square

<button on:click={initialize}>
Regenerate
</button>
