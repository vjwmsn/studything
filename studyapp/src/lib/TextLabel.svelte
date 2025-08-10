<script>
    let {content = "TextLabel", align = ""} = $props()
</script>

<div class="textLabel {align}">{content}</div>

<style>

    .textLabel {
        border: 0px;
        border-radius: 10px;
        background: linear-gradient(hsl(0, 0%, 100%), hsl(0,0%,90%));
        filter: drop-shadow(0 0 0.15rem hsl(257, 90%, 50%));
        padding: 10px;
        color: hsl(0, 0%, 25%);
        margin-left: 5px;
        margin-right: 5px;
        text-align: center;
        font-family: "Mozilla Text", "sans-serif";
        font-weight: 800;
    }

    .right {
        margin-left: auto;
    }

    .fill-stretch {
        flex: 1;
        margin-left: 5px;
        margin-right: 10px;
    }

</style>