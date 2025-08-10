<script>
import ButtonS from "$lib/TextButton.svelte"
import TextLabel from "$lib/TextLabel.svelte"
import Bar from "$lib/Bar.svelte"

let count = $state(0)

function sayHello () {
    count++
    console.log(count)
}


</script>


<div class="body">
<ButtonS content={count} onClick={sayHello}/>
<TextLabel content="Hello World"/>
<Bar>
    <ButtonS content="Hello, i'm inside a bar"/>
    <TextLabel content="Me too!"/>
</Bar>
</div>

<style>
    .body {
        background-color: hsl(0,0%,90%);
    }
</style>