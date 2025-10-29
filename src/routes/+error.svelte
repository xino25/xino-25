<script>
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';
</script>

<svelte:head>
	<title>{$page.status} - Error | XINO</title>
</svelte:head>

<div class="min-h-screen flex items-center justify-center px-4">
	<div class="max-w-2xl w-full text-center bg-white/10 backdrop-blur-lg rounded-2xl shadow-xl p-12 border border-green-500/20">
		<!-- Error Code with Green Glow Effect -->
		<div class="relative mb-8">
			<h1 class="text-9xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-green-400 via-teal-400 to-cyan-400 animate-pulse">
				{$page.status}
			</h1>
			<div class="absolute inset-0 text-9xl font-bold text-green-500 opacity-10 blur-md animate-ping">
				{$page.status}
			</div>
		</div>

		<!-- Error Message -->
		<h2 class="text-3xl md:text-4xl font-bold text-white mb-4">
			{#if $page.status === 404}
				Page Not Found
			{:else if $page.status === 500}
				Internal Server Error
			{:else}
				Something Went Wrong
			{/if}
		</h2>

		<p class="text-gray-300 text-lg mb-8 max-w-lg mx-auto">
			{#if $page.status === 404}
				The page you're looking for seems to have vanished into the digital void. Let's get you back on track!
			{:else if $page.status === 500}
				Our servers encountered an unexpected error. Don't worry, we're on it!
			{:else}
				An unexpected error occurred. We're working to fix it.
			{/if}
		</p>

		<!-- Action Buttons -->
		<div class="flex flex-col sm:flex-row gap-4 justify-center items-center">
			<button
				on:click={() => goto('/')}
				class="px-8 py-3 bg-gradient-to-r from-green-500 to-teal-500 hover:from-green-600 hover:to-teal-600 text-white font-semibold rounded-lg shadow-lg transform transition hover:scale-105 active:scale-95"
			>
				← Back to Home
			</button>
			<button
				on:click={() => window.history.back()}
				class="px-8 py-3 bg-white/10 hover:bg-white/20 text-white font-semibold rounded-lg shadow-lg transform transition hover:scale-105 active:scale-95 border border-green-500/30"
			>
				Go Back
			</button>
		</div>

		<!-- Decorative Elements -->
		<div class="mt-16 grid grid-cols-3 gap-4 max-w-md mx-auto opacity-30">
			<div class="h-2 bg-green-500 rounded-full animate-pulse"></div>
			<div class="h-2 bg-teal-500 rounded-full animate-pulse delay-75"></div>
			<div class="h-2 bg-cyan-500 rounded-full animate-pulse delay-150"></div>
		</div>


	</div>
</div>

<style>
	@keyframes ping {
		75%, 100% {
			transform: scale(1.1);
			opacity: 0;
		}
	}

	.animate-ping {
		animation: ping 2s cubic-bezier(0, 0, 0.2, 1) infinite;
	}

	.delay-75 {
		animation-delay: 75ms;
	}

	.delay-150 {
		animation-delay: 150ms;
	}

	@keyframes ping {
		75%, 100% {
			transform: scale(1.1);
			opacity: 0;
		}
	}

	.animate-ping {
		animation: ping 2s cubic-bezier(0, 0, 0.2, 1) infinite;
	}

	.delay-75 {
		animation-delay: 75ms;
	}

	.delay-150 {
		animation-delay: 150ms;
	}
</style>
