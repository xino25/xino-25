<script>
	import favicon from '$lib/assets/favicon.svg';
	import bg from '$lib/assets/bg2.png';
	import { Navbar } from '$lib';
	import '../app.css';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<main class="relative container h-screen w-screen bg-cover bg-center bg-fixed pl-72" style="background-image: url({bg});">
	<!-- Background opacity overlay -->
	<div class="absolute inset-0 bg-black/25 backdrop-blur-[2px] pointer-events-none"></div>
	
	<Navbar />
	<div class="relative z-10 h-full p-8">
		{@render children?.()}
	</div>
</main>
