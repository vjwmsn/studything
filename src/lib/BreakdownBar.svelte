<script>
	let {
		zones = [
			{ name: 'Zone1', percentage: 30, bg: 'blue' },
			{ name: 'Zone2', percentage: 70, bg: 'red' }
		]
	} = $props();
</script>

<div class="progressBar">
	{#each zones as zone, i (zone.name)}
		<div
			class="progress_fill"
			style="width: {zone.percentage}%; background: {zone.bg};"
		>
			<span class="progress_span notouchy">
				{zone.name} - {zone.percentage}%
			</span>
		</div>
	{/each}
</div>

<style>
    
	.progressBar {
		display: flex; 
		align-items: center;
		border-radius: 10px;
		background: linear-gradient(hsl(0, 0%, 100%), hsl(0, 0%, 90%));
		filter: drop-shadow(0 0 0.05rem hsl(0, 0%, 24%));
		padding: 0; 
		color: var(--color-bg-dark-start); 
        height: auto;
		text-align: center;
		font-family: 'Mozilla Text', 'sans-serif';
		font-weight: 800;
		height: 2rem; 
		position: relative;
		overflow: hidden;
	}

	.progress_fill {
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: all 0.2s;
	}

    .progress_fill:hover {
        box-shadow: inset 0px 0px 5px hsl(0, 0%, 35%);
        filter: drop-shadow(0 0 0.05rem hsl(0, 0%, 24%));
    }

	.progress_fill:first-child {
		border-top-left-radius: 10px;
		border-bottom-left-radius: 10px;
	}

	.progress_fill:last-child {
		border-top-right-radius: 10px;
		border-bottom-right-radius: 10px;
	}

	.progress_span {
		user-select: none;
	}
</style>