<script>
    let {content = "Button", onClick, align=""} = $props()


    function handleClick () {
        onClick?.();
    }

</script>

<button class="regular-button {align}" onclick={handleClick}>{content}</button>

<style>
    .regular-button {
        border: 0;
        border-radius: 10px;
        background: linear-gradient(hsl(257, 90%, 50%),hsl(257, 90%, 35%));
        padding: 10px;
        color: hsl(0, 0%, 95%);
        opacity: 100%;
        transition: 0.3s;
        filter: drop-shadow(0 0 0.15rem hsl(257, 90%, 50%));
        font-weight: 800;
        font-family: "Mozilla Text", "sans-serif";
        margin-left: 5px;
        margin-right: 5px;
        text-align: center; 
        transition: all 0.3s;
   
    }

    .regular-button:hover {filter: drop-shadow(0 0 0.25rem hsl(257, 100%, 50%)) brightness(120%); cursor: pointer; background: linear-gradient(hsl(257, 90%, 50%),hsl(257, 90%, 35%));}

    .regular-button:active {filter:  drop-shadow(0 0 0.15rem hsl(257, 100%, 50%)) brightness(90%); cursor: pointer; transition: all 0.1s;}

    .right {
        margin-left: auto;
    }

    .center {
        margin-left: auto;
        margin-right: auto;
    }

</style>