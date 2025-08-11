<script>
    let {children} = $props()
</script>

<div class="bar">
    {@render children()}
</div>

<style>
    .bar {
        display: flex;
        flex-direction: row;
        align-items: center;
        min-height: 3rem;
        max-height: 3rem;
        background: linear-gradient(hsl(0,0%,95%), hsl(0,0%,88%));
        padding: 10px;
    }
</style>