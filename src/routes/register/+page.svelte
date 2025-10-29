<script>
	import { onMount } from 'svelte';
	
	const url = 'https://docs.google.com/forms/d/e/1FAIpQLScKyi1kBuy2HGFURSpYewuGBQjE4pdcaIT3F-Yqw9_t69fS8g/viewform?usp=sharing&ouid=109031010375823453407';
	
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
