<script>
	function openReel(url) {
		window.open(url, '_blank');
	}
</script>

<div class="min-h-screen flex items-center justify-center">
	<div class="flex flex-col gap-8">
		<button class="bg-gradient-to-r from-emerald-600 to-emerald-500 hover:from-emerald-500 hover:to-emerald-400 text-white font-semibold px-8 py-4 rounded-lg shadow-lg hover:shadow-emerald-500/50 transition-all duration-300 transform hover:scale-105"
			on:click={() => openReel('https://www.instagram.com/reel/C89GJEwpoRX/')}
		>
			Watch Reel 1
		</button>
		
		<button class="bg-gradient-to-r from-emerald-600 to-emerald-500 hover:from-emerald-500 hover:to-emerald-400 text-white font-semibold px-8 py-4 rounded-lg shadow-lg hover:shadow-emerald-500/50 transition-all duration-300 transform hover:scale-105"
			on:click={() => openReel('https://www.instagram.com/famous_ram/reel/DJPCrVcSX3Y/')}
		>
			Watch Reel 2
		</button>
		
		<button class="bg-gradient-to-r from-emerald-600 to-emerald-500 hover:from-emerald-500 hover:to-emerald-400 text-white font-semibold px-8 py-4 rounded-lg shadow-lg hover:shadow-emerald-500/50 transition-all duration-300 transform hover:scale-105"
			on:click={() => openReel('https://www.instagram.com/reel/DQMjhhbjF7K/?igsh=MXFkOHRuaHR3dHAwaQ==')}
		>
			Watch Reel 3
		</button>
	</div>
</div>
