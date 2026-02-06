<script>
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
	import { base } from '$app/paths';
</script>


<nav> 
	<a href="{base}/">Hem</a>
	<a href="{base}/photoapp">Photo app</a>
	<a href="{base}/register">Register</a>
	<a href="{base}/shoppinglist">Shopping list</a>
	<a href="{base}/memory">Memory</a>
	<a href="{base}/chat">Chat</a>
	<a href="{base}/search">Search</a>
</nav>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children?.()}

<style>

	:global(body), :global(html){
  		margin: 0%;
  		padding: 0%;
  		height: 100vh;
  		width: 100vw;
	}    
</style>