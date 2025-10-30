<svelte:head>
	<title>XINO | Members</title>
</svelte:head>

<script>
	// Members page
	import { onMount } from 'svelte';
	
	let currentView = 'members'; // 'members' or 'alumni'
	let imageCache = new Map(); // Cache for preloaded images
	let loadingStates = new Map(); // Track loading states

	// Sample members data - replace with actual data
	const members = [
		// Core Team
		{ name: 'Udbhav Jha', designation: 'President' },
		{ name: 'Vihaan Kulkarni', designation: 'President' },
		{ name: 'Aarav Rajpal', designation: 'Vice President' },
		{ name: 'Avni Tiwari', designation: 'Vice President' },
		{ name: 'Ruhaan Gilautra', designation: 'Secretary' },
		{ name: 'Laksh Kapoor', designation: 'Secretary' },

		// Heads of Departments
		{ name: 'Rishit Narang', designation: 'Head Programming' },
		{ name: 'Arnav Bhargava', designation: 'Head Surprise' },
 		// { name: 'Arul Gandhi', designation: 'Head Hardware' },
		 { name: 'Bhavya SK', designation: 'Head Quiz' },
		{ name: 'Param Sen', designation: 'Head Crossword' },
		{ name: 'Akshar Gupta', designation: 'Head Machine Learning' },
		
		// Members
		// { name: 'Rishit Soneja', designation: 'Member' },
		{ name: 'Harshit Malhotra', designation: 'Member' },
		{ name: 'Arnav Jain', designation: 'Member' },
		{ name: 'Mayank Swami', designation: 'Member' },
		{ name: 'Archita Tiwari', designation: 'Member' },
	];

	// Sample alumni data - replace with actual data
	const alumni = [
		// Batch 2024-25
		{ name: "Anirudh Dabas", designation: "President 24-25", image: "anirudh.jpg" },
		{ name: "Akshatt Dahiya", designation: "Vice President 24-25", image: "akshatt_n.png" },
		
		// Batch 2023-24
		{ name: "Tijil Chabbra", designation: "President 23-24", image: "tijil.png" },
		{ name: "Aurum Mandal", designation: "President 23-24", image: "aurum mandal.png" },
		{ name: "Ekansh Arora", designation: "President 23-24", image: "Ekaansh Arora.jpg" },
		{ name: "Abhishree Bhardwaj", designation: "President 23-24", image: "abhishree.jpg" },
		{ name: "Nishchay Bhatia", designation: "Vice President 23-24", image: "Nischay Bhatia.png" },
		{ name: "Arnav Gupta", designation: "Vice President 23-24", image: "Arnav Gupta.jpg" },
		{ name: "Kriti Grover", designation: "Head Design 23-24", image: "Kriti grover.png" },
		{ name: "Yuvaan Mutreja", designation: "Head Hardware 23-24", image: "yuvaan_3.png" },

		// Batch 2022-23
		{ name: "Anant Gupta", designation: "President 22-23", image: "anant.png" },
		{ name: "Arnav Shukla", designation: "Head Hardware 22-23", image: "arnav_shukla.png" },

		// Batch 2021-22
		{ name: "Shaurya Bajaj", designation: "President 21-22", image: "shaurya bajaj.png" },
		{ name: "Manit Kaushik", designation: "President 21-22", image: "manit kaushik.png" },
		{ name: "Moaksh Kakkar", designation: "Vice President 21-22", image: "moaksh kakkar.png" },
		{ name: "Shaunak Sachdev", designation: "Vice President 21-22", image: "shaunak sachdev.png" }
	];

	$: currentData = currentView === 'members' ? members : alumni;

	function toggleView(view) {
		currentView = view;
	}

	function getImageName(name) {
		// Create mapping for known images
		const imageMap = {
			'Udbhav Jha': 'udbhav.jpg',
			'Vihaan Kulkarni': 'vihaan_kulkarni.png',
			'Dhruv Dewan': 'dhruv dewan_2.jpg',
			'Aarav Rajpal': 'aarav_rajpal.jpg',
			'Avni Tiwari': 'avni_tiwari.jpg',
			'Laksh Kapoor': 'laksh.jpg',
			'Rishit Narang': 'rishit_goat.jpg',
			'Avi Rana': 'avi_rana.jpg',
			'Tejas Jain': 'tejas_jain.jpg',
			'Ruhaan Gilautra': 'ruhaan.jpg',
			'Bhavya SK': 'bhavya_sk.jpg',
			'Harshit Malhotra': 'harshit.jpg',
			'Mayank Swami': 'mayank.jpg',
			'Akshar Gupta': 'akshar.jpeg',
			'Arnav Jain': 'arnav jain.jpeg',
			'Arnav Bhargava': 'arnav bhargava.jpg',
			'Param Sen': 'param sen.jpg',
			'Archita Tiwari': 'archita.jpg'
		};
		
		return imageMap[name] || 'default.png';
	}

	function getAlumniImagePath(person) {
		// For alumni, use the provided image filename
		return person.image ? `/alumni/${person.image}` : '/alumni/default.png';
	}



	// Enhanced image loading with cache
	function getImageSrc(person) {
		const src = currentView === 'members' 
			? `/members/${getImageName(person.name)}` 
			: getAlumniImagePath(person);
		
		// Return cached image if available, otherwise return src for normal loading
		return  src;
	}
</script>

<div class="min-h-screen p-6">


	<!-- Toggle Switch with External Labels -->
	<div class="flex justify-center items-center gap-1 sm:gap-2 mb-12" >
		<!-- Members Label -->
		<button 
			class="text-sm sm:text-base md:text-lg font-medium transition-colors duration-300 px-2 sm:px-3 md:px-4 py-2 cursor-pointer"
			class:text-white={currentView === 'members'}
			class:text-gray-400={currentView === 'alumni'}
			on:click={() => currentView = 'members'}
		>
			Members
		</button>
		
		<!-- Toggle Switch Body -->
		<div 
			class="relative bg-gray-700 rounded-full w-14 sm:w-16 h-7 sm:h-8 cursor-pointer flex-shrink-0"
			role="button"
			tabindex="0"
			on:click={() => currentView = currentView === 'members' ? 'alumni' : 'members'}
			on:keydown={(e) => e.key === 'Enter' && (currentView = currentView === 'members' ? 'alumni' : 'members')}
		>
			<!-- Sliding Knob -->
			<div 
				class="absolute top-1 left-1 w-5 sm:w-6 h-5 sm:h-6 bg-green-500 rounded-full shadow-lg transition-transform duration-300 ease-in-out"
				class:translate-x-7={currentView === 'alumni'}
				class:sm:translate-x-8={currentView === 'alumni'}
			></div>
		</div>
		
		<!-- Alumni Label -->
		<button 
			class="text-sm sm:text-base md:text-lg font-medium transition-colors duration-300 px-2 sm:px-3 md:px-4 py-2 cursor-pointer"
			class:text-white={currentView === 'alumni'}
			class:text-gray-400={currentView === 'members'}
			on:click={() => currentView = 'alumni'}
		>
			Alumni
		</button>
	</div>

	<!-- Members/Alumni Grid -->
	<div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-12 max-w-6xl mx-auto">
		{#each currentData as person, index}
			<div 
				class="bg-blur rounded-lg hover:scale-105 transition-all hover:shadow-xl group overflow-hidden"
				data-aos="fade-up"
				data-aos-delay="{index * 30}"
			>
				<!-- Avatar with Image and Text Overlay -->
				 <!-- image transition control -->
				<div 
					class="w-full h-auto aspect-[4/5] rounded-lg group-hover:scale-105 transition-all duration-400 ease-out overflow-hidden shadow-xl will-change-transform bg-black relative pb-8"
				>
					<img 
						src="{getImageSrc(person)}" 
						alt="{person.name}"
						class="w-full h-full object-cover rounded-lg transform-gpu opacity-100 group-hover:scale-110 transition-transform duration-500 ease-out"
						loading="lazy"
						decoding="async"
						on:error={(e) => {
							// Enhanced error handling with proper fallback
							const defaultSrc = currentView === 'members' ? '/members/default.png' : '/alumni/default.png';
							if (e.target.src !== defaultSrc) {
								e.target.src = defaultSrc;
							}
						}}
					/>
					
					<!-- Progressive Blur Overlay -->
					<div class="progressive-blur-overlay absolute inset-0 rounded-lg overflow-hidden"></div>
					
					<!-- Person Info Overlay -->
					<div class="absolute bottom-0 left-0 right-0 p-3 text-center z-10 group-hover:-translate-y-2 -translate-y-3 transition-transform duration-500 ease-out">
						<h3 class="text-emerald-400 font-semibold text-lg mb-1 group-hover:text-emerald-300 group-hover:scale-105 transition-all duration-500 ease-out drop-shadow-lg">
							{person.name}
						</h3>
						<p class="text-white text-sm font-medium group-hover:scale-105 transition-all duration-500 ease-out drop-shadow-md">
							{person.designation}
						</p>
					</div>
				</div>
			</div>
		{/each}
	</div>

	<!-- Empty State -->
	{#if currentData.length === 0}
		<div class="text-center py-16">
			<div class="bg-blur rounded-lg p-8 max-w-md mx-auto">
				<h3 class="text-white text-xl font-semibold mb-2">No {currentView} found</h3>
				<p class="text-white/70">Check back later for updates.</p>
			</div>
		</div>
	{/if}
</div>

<style>
	/* Ensure member images are fully opaque */
	img {
		opacity: 1 !important;
	}

	/* Progressive blur effect from 0 to 8px top to bottom */
	.progressive-blur-overlay {
		background: linear-gradient(
			to bottom,
			transparent 0%,
			transparent 60%,
			rgba(0, 0, 0, 0.1) 70%,
			rgba(0, 0, 0, 0.3) 80%,
			rgba(0, 0, 0, 0.5) 90%,
			rgba(0, 0, 0, 0.7) 100%
		);
		backdrop-filter: blur(0px);
		-webkit-backdrop-filter: blur(0px);
	}

	/* Create progressive blur using multiple layers */
	.progressive-blur-overlay::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(
			to bottom,
			transparent 0%,
			transparent 60%,
			rgba(0, 0, 0, 0.1) 70%,
			rgba(0, 0, 0, 0.2) 80%,
			rgba(0, 0, 0, 0.3) 90%,
			rgba(0, 0, 0, 0.4) 100%
		);
		backdrop-filter: blur(2px);
		-webkit-backdrop-filter: blur(2px);
	}

	.progressive-blur-overlay::after {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(
			to bottom,
			transparent 0%,
			transparent 70%,
			rgba(0, 0, 0, 0.1) 80%,
			rgba(0, 0, 0, 0.2) 90%,
			rgba(0, 0, 0, 0.3) 100%
		);
		backdrop-filter: blur(8px);
		-webkit-backdrop-filter: blur(8px);
	}
</style>

