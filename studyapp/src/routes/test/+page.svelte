<script>
import ButtonS from "$lib/TextButton.svelte"
import TextLabel from "$lib/TextLabel.svelte"

let count = $state(0)

function sayHello () {
    count++
    console.log(count)
}


</script>


<div class="body">
<ButtonS content={count} onClick={sayHello}/>
<TextLabel content="Hello World"/>
</div>

<style>
    .body {
        background-color: hsl(0,0%,90%);
    }
</style>