<script>
	import { onMount } from 'svelte';
	
	const url = 'https://docs.google.com/forms/d/e/1FAIpQLSeJBR56O_HtiZW1yPxS1OWvuIztA2hlko97fgS5LVh9eScDVw/viewform?usp=sharing&ouid=109031010375823453407';
	
	onMount(() => {
		window.location.href = url;
	});
</script>

<svelte:head>
	<meta http-equiv="refresh" content="0; url={url}" />
</svelte:head>

<div class="flex items-center justify-center min-h-screen">
	<p class="text-2xl font-gray-700 font-bold">Redirecting to XCrypt registration...</p>
</div>
