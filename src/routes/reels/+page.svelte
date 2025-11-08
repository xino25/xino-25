<script>
	function openReel(url) {
		window.open(url, '_blank');
	}
</script>

<div class="min-h-screen flex items-center justify-center">
	<div class="flex flex-col gap-12">
		<button class="bg-black px-4 py-2 border-black"
			on:click={() => openReel('https://www.instagram.com/reel/C89GJEwpoRX/')}
		>
			Reel 1
		</button>
		
		<button class="bg-black px-4 py-2 border-black"
			on:click={() => openReel('https://www.instagram.com/famous_ram/reel/DJPCrVcSX3Y/')}
		>
			Reel 2
		</button>
	</div>
</div>
