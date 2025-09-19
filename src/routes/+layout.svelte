<script>
	import favicon from '$lib/assets/favicon.svg';
	import bg from '$lib/assets/bg2.png';
	import { Navbar, Sidebar } from '$lib';
	import '../app.css';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<main class="relative min-h-screen w-full bg-cover bg-center bg-fixed lg:pl-32 lg:pr-80 text-white" style="background-image: url({bg});">
	<!-- Background opacity overlay -->
	<div class="absolute inset-0 bg-black/20 backdrop-blur-[1px] pointer-events-none"></div>
	
	<Navbar />
	<Sidebar />
	<div class="relative h-full w-full p-8 lg:p-8 pt-24 lg:pt-8">
		{@render children?.()}
	</div>


	
	<script type="module" src="https://unpkg.com/ionicons@7.1.0/dist/ionicons/ionicons.esm.js"></script>
	<script nomodule src="https://unpkg.com/ionicons@7.1.0/dist/ionicons/ionicons.js"></script>
</main>


