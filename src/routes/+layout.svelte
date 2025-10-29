<script>
	const bg = '/assets/logos/bg2.png';
	import { Navbar, Sidebar } from '$lib';
	import '../app.css';
	import { onMount } from 'svelte';
	import AOS from 'aos';
	import 'aos/dist/aos.css';
	import { page } from '$app/stores';
	import { browser } from '$app/environment';

	let { children } = $props();

	onMount(() => {
		AOS.init({
			duration: 600,
			easing: 'ease-out',
			once: true,
			offset: 50
		});
	});


	let isinfopage = $derived(browser && $page.url.pathname === '/info');
	
	// Debug logging effect
	$effect(() => {
		if (browser) {
			console.log('Current pathname:', $page.url.pathname);
			console.log('isInfoPage:', isinfopage);
		}
	});

</script>

<svelte:head>
	<link rel="icon" href="/assets/logos/xino logo.png" />
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Source+Sans+3:ital,wght@0,200..900;1,200..900&display=swap" rel="stylesheet">
</svelte:head>

<main class="relative min-h-screen w-full bg-cover bg-center bg-fixed lg:pl-32 text-white font-['Source Sans 3']" style="background-image: url({bg});" class:lg:pr-80={!isinfopage}>
	<!-- Background opacity overlay -->
	<div class="absolute inset-0 bg-black/20 backdrop-blur-[1px] pointer-events-none"></div>
	
	<Navbar />
	{#if !isinfopage}
		<Sidebar />
	{/if}
	<div class="relative h-full w-full p-8 lg:p-8 pt-24 lg:pt-8">
		{@render children?.()}
	</div>


	
	<script type="module" src="https://unpkg.com/ionicons@7.1.0/dist/ionicons/ionicons.esm.js"></script>
	<script nomodule src="https://unpkg.com/ionicons@7.1.0/dist/ionicons/ionicons.js"></script>
</main>


