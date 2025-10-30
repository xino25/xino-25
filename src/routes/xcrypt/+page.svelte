<script>
	import { onMount } from 'svelte';
	
	const url = 'https://xcrypt.xino.in';
	
	onMount(() => {
		window.location.href = url;
	});
</script>

<svelte:head>
	<meta http-equiv="refresh" content="0; url={url}" />
</svelte:head>

<div class="flex items-center justify-center min-h-screen">
	<p class="text-2xl font-gray-700 font-bold">Redirecting to registration form...</p>
</div>
