<script>
    let {
        value = $bindable(""),
        placeholder = "",
        isDisabled = false,
        onEnterUp = null,
    } = $props();
</script>

<div class="container">
    <input
        bind:value
        class="input"
        type="text"
        placeholder={placeholder}
        disabled={isDisabled}
        onkeyup={(e) => {
            if (e.key === "Enter" && typeof onEnterUp === "function") {
                onEnterUp(e);
            }
        }}
    >
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        flex-grow: 1;
        width: auto;
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
        filter: drop-shadow(0 0 0.05rem hsl(0, 0%, 18%));
    }
    .input:focus {
        filter: drop-shadow(0 0 0.25rem hsl(257, 100%, 50%));
        outline: 0;
    }
</style>
