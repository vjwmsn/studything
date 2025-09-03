<script>
	import favicon from '$lib/assets/favicon.png';

	let { children } = $props();
</script>

<svelte:head>


	<link rel="icon" href={favicon} />

	<style>
	@import url('https://fonts.googleapis.com/css2?family=Mozilla+Text:wght@200..700&display=swap');
	</style>


</svelte:head>

<style>
	:global(body) {
		margin: 0;
		background-color: hsl(0%, 0% 90%);
		font-family: "Mozilla Text", sans-serif;
	}

	:global(:root) {
		--color-accent-1: hsl(257, 100%, 50%);
		--color-accent-1-90-50: hsl(257, 90%, 50%);
		--color-accent-1-90-35: hsl(257, 90%, 35%);
		--color-accent-green: hsl(145, 100%, 70%);
		--color-accent-red: hsl(4, 100%, 50%);
		--color-bg-start: hsl(0, 0%, 100%);
		--color-bg-end: hsl(0, 0%, 90%);
		--color-bg-dark-start: hsl(0, 0%, 15%);
		--color-bg-dark-end: hsl(0, 0%, 25%);
	}
	
</style>

{@render children?.()}
