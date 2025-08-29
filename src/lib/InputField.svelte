<script>
    // still mad about export let
    let {
        value = $bindable(""),
        placeholder = "",
        isDisabled = false
        } = $props()

</script>

<div class="container">
    <input bind:value class="input" type="text" placeholder={placeholder} disabled={isDisabled}>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .input {
        border: 0px;
        border-radius: 5px;
        padding: 10px;
        font-size: x-large;
        font-weight: 600;
        font-family: "Mozilla Text", sans-serif;
        transition: 0.3s;
        margin: 5px;
        width: auto;
    }

    .input:focus {
        filter: drop-shadow(0 0 0.25rem hsl(257, 100%, 50%));
        outline: 0;
    }
    

</style>