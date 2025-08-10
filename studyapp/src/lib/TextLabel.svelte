<script>
    let {content = "TextLabel"} = $props()
</script>

<div class="textLabel">{content}</div>

<style>

    .textLabel {
        border: 0px;
        border-radius: 10px;
        background: linear-gradient(hsla(0, 0%, 50%, 0.2), hsla(0,0%,50%, 0.1));
        padding: 10px;
        color: hsl(0, 0%, 25%);
        margin-left: 5px;
        margin-right: 5px;
        text-align: center;
        max-width: fit-content;
        font-family: "Mozilla Text", "sans-serif";
        font-weight: 800;
    }
</style>