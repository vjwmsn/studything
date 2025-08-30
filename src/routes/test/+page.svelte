<script>
import ButtonS from "$lib/TextButton.svelte"
import TextLabel from "$lib/TextLabel.svelte"
import Bar from "$lib/Bar.svelte"
import InputField from "$lib/InputField.svelte";
import ProgressBar from "$lib/ProgressBar.svelte";

let progress = $state(0)

let count = $state(0)

function sayHello () {
    count++
    console.log(count)
}


</script>


<div class="body">
<ButtonS content={count} onClick={sayHello}/>
<ProgressBar content="I'm a progress bar" progress={progress}/>
<Bar>
    <ButtonS content="Hello, i'm inside a bar"/>
    <TextLabel content="Me too!"/>
    <InputField bind:value={progress} placeholder="Change the progress bar with me!"/>
</Bar>
</div>

<style>
    .body {
        background-color: hsl(0,0%,90%);
    }
</style>