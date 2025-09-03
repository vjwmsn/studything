<script>
import ButtonS from "$lib/TextButton.svelte"
import TextLabel from "$lib/TextLabel.svelte"
import Bar from "$lib/Bar.svelte"
import InputField from "$lib/InputField.svelte";
import ProgressBar from "$lib/ProgressBar.svelte";
import ConvertingPoint from "$lib/ConvertingPoint.svelte";

let progress = $state(0)

let count = $state(0)

let active = $state(false)

function sayHello () {
    count++
    console.log(count)
}

function toggleActive() {
    active = !active
}

</script>


<div class="body">
<ButtonS content={count} onClick={sayHello}/>
<ProgressBar content="I'm a progress bar" progress={progress}/>
<Bar>
    <ButtonS content="Hello, i'm inside a bar. Click on me to toggle the thing" onClick={toggleActive}/>
    <TextLabel content="I'm a text label in a bar!!"/>
    <InputField bind:value={progress} placeholder="Change the progress bar with me!"/>
    <ConvertingPoint active={active} size="30px"/>
</Bar>
</div>

<style>
    .body {
        background-color: hsl(0,0%,90%);
    }
</style>