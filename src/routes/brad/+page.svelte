<script>
    import BreakdownBar from "$lib/BreakdownBar.svelte";
</script>

<BreakdownBar zones={[
    { name: 'Correct', percentage: 30, bg: 'var(--color-accent-green)' },
    { name: 'Wrong', percentage: 30, bg: 'var(--color-accent-red)'},
    { name: 'Skipped', percentage: 40, bg: 'var(--color-accent-yellow)' }
    
    ]} />