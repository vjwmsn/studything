<script>
	import favicon from '$lib/assets/favicon.svg';

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
		background-color: hsl(0%, 0% 100%);
		font-family: "Mozilla Text", sans-serif;
	}
	
</style>

{@render children?.()}
