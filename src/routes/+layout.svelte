<script>
	import favicon from '$lib/assets/favicon.svg';
	import {base} from '$app/paths';

	let { children } = $props();

	
</script>

<nav>
	<a href="{base}/">Hem</a>
	<a href="{base}/photoapp">Photo App</a>
	<a href="{base}/register">Register</a>
	<a href="{base}/shoppinglist">Shoppinglist</a>
	<a href="{base}/memory">Memory</a>
	<a href="{base}/chat">Chat</a>
	<a href="{base}/search">Search</a>
	<a href="{base}/prov">Prov</a>
	<a href="{base}/badUX">Bad UX</a>
	<a href="{base}/inputOS">Input OS</a>
	<a href="{base}/gameExpTest">Shadows Challenge</a>
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
