<script>
    let {children} = $props()
</script>

<div class="table">
    {@render children()}
</div>

<style>
    .table {
        height: auto;
        width: 50%;
        margin-top: 15px;
    }
</style>