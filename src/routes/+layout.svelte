<script>
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();

	
</script>

<nav>
	<a href="/">Hem</a>
	<a href="/photoapp">Photo App</a>
	<a href="/register">Register</a>
	<a href="/shoppinglist">Shoppinglist</a>
</nav>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<style>
	:global(body), :global(html){
  		margin: 0%;
  		padding: 0%;
  		height: 100vh;
  		width: 100vw;
	}    
</style>

{@render children?.()}
