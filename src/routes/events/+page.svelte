<svelte:head>
	<title>XINO | Events</title>
</svelte:head>

<script>
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	
	// Events data structure
	const events = [
		// Creative Events
		{
			name: "Xquisite",
			description: "All-round creative hackathon and design challenge testing participants' skills in various domains",
			type: "Creative",
			keywords: ["creative", "hackathon", "design", "web dev", "UI/UX"]
		},
		
		// Discussion Events
		{
			name: "Xclamation Point!",
			description: "Group discussion and debate competition",
			type: "Discussion",
			keywords: ["discussion", "gd", "grp"]
		},
		
		// Programming Events
		{
			name: "eXecute.eXe",
			description: "Competitive programming challenge on hackerrank",
			type: "Programming",
			keywords: ["programming", "coding", "competitive", "cp", "dsa"]
		},
		
		// Surprise Events
		{
			name: "Xclusive",
			description: "Mystery surprise event ",
			type: "Surprise",
			keywords: ["surprise", "mystery", "exclusive", "unexpected", "challenge"]
		},
		
		// Quiz Events
		{
			name: "techXult Jr.",
			description: "Junior level technology quiz competition",
			type: "Quiz",
			keywords: ["quiz", "junior"]
		},
		{
			name: "techXult Sr.",
			description: "Senior level technology quiz competition",
			type: "Quiz", 
			keywords: ["quiz", "senior"]
		},
		
		// Cube Solving Events
		{
			name: "XCube 2x2",
			description: "2x2 Rubik's cube solving competition",
			type: "Cubing",
			keywords: ["cube", "2x2", "rubiks", "solving", "puzzle", "cubing"]
		},
		{
			name: "XCube 3x3",
			description: "3x3 Rubik's cube solving competition",
			type: "Cubing",
			keywords: ["cube", "3x3", "rubiks", "solving", "cubing", "puzzle"]
		},
		{
			name: "XCube Pyraminx",
			description: "Pyraminx cube solving competition",
			type: "Cubing",
			keywords: ["cube", "pyraminx", "solving", "cubing", "puzzle"]
		},
		
		// Film Making Events
		{
			name: "XFrame",
			description: "Online film making competition",
			type: "Film Making",
			keywords: ["film", "making", "video", "online", "creative"]
		},
		
		// Robotics Events
		{
			name: "autoForge",
			description: "Robothon - robotics design and automation challenge",
			type: "Robotics",
			keywords: ["robotics", "automation", "robothon", "engineering", "hardware"]
		},
		
		// Machine Learning Events
		{
			name: "autoCognito",
			description: "Online machine learning and AI challenge",
			type: "Machine Learning",
			keywords: ["machine", "learning", "AI", "artificial", "intelligence", "online", "data"]
		},
		
		// Cryptic Hunt Events
		{
			name: "XCrypt",
			description: "Cryptic hunt",
			type: "Cryptic Hunt",
			keywords: ["cryptic", "hunt", "puzzles", "clues", "mystery", "solving"]
		}
	];

	// Search functionality
	let searchTerm = '';
	let filteredEvents = events;
	let searchPlaceholder = 'Search events by name, type, or keywords...';
	
	// Image preloading and caching - removed since using gradient backgrounds
	const imageCache = new Map();
	
	onMount(() => {
		// Set initial placeholder based on window width
		updatePlaceholder();
		
		// Update placeholder on window resize
		window.addEventListener('resize', updatePlaceholder);
		
		return () => {
			window.removeEventListener('resize', updatePlaceholder);
		};
	});
	
	// Update placeholder text based on screen size
	function updatePlaceholder() {
		if (window.innerWidth < 640) { // sm breakpoint is 640px
			searchPlaceholder = 'Search by name, type, or keywords...';
		} else {
			searchPlaceholder = 'Search events by name, type, or keywords...';
		}
	}
	
	// Get optimized image source - simplified since using gradients
	function getImageSrc(event) {
		return '/members/default.png';
	}
	
	// Search filter function
	function filterEvents() {
		if (!searchTerm.trim()) {
			filteredEvents = events;
			return;
		}
		
		const searchLower = searchTerm.toLowerCase();
		filteredEvents = events.filter(event => 
			event.name.toLowerCase().includes(searchLower) ||
			event.type.toLowerCase().includes(searchLower) ||
			event.description.toLowerCase().includes(searchLower) ||
			event.keywords.some(keyword => keyword.toLowerCase().includes(searchLower))
		);
	}
	
	// Reactive statement for search
	$: {
		searchTerm;
		filterEvents();
	}
</script>

<!-- Search Bar -->
<div class="mb-8 flex justify-center py-12">
	<div class="relative w-full max-w-md">
		<input
			bind:value={searchTerm}
			type="text"
			placeholder="{searchPlaceholder}"
			class="w-full px-4 py-3 bg-white/10 backdrop-blur-md border border-white/20 rounded-xl text-white placeholder-white/60 focus:outline-none focus:ring-2 focus:ring-emerald-400 focus:border-transparent transition-all duration-200"
		/>
		<div class="absolute right-3 top-1/2 transform -translate-y-1/2 text-white/60">
			<ion-icon name="search-outline"></ion-icon>
		</div>
	</div>
</div>

<!-- Events Grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
	{#each filteredEvents as event (event.name)}
		<div 
			class="relative bg-blur rounded-xl overflow-hidden hover:scale-105 transition-transform duration-300 cursor-pointer group flex flex-col"
			in:fly="{{ y: 50, duration: 300, delay: Math.min(filteredEvents.indexOf(event) * 100, 800) }}"
		>
			<!-- Background Image -->
			<div 
				class="absolute inset-0 bg-gradient-to-br from-emerald-600/20 to-blue-600/20"
			>
				<div class="absolute inset-0 bg-black/50 group-hover:bg-black/40 transition-colors duration-300"></div>
			</div>
			
			<!-- Content Overlay -->
			<div class="relative p-6 h-48 flex flex-col justify-center">
				<h3 class="text-white text-xl font-bold mb-2">
					{event.name}
				</h3>
				<p class="text-white/80 text-sm mb-3">
					{event.description}
				</p>
				<div class="mt-2 inline-block">
					<span class="bg-emerald-500/20 text-emerald-300 px-2 py-1 rounded-full text-xs">
						{event.type}
					</span>
				</div>
			</div>
		</div>
	{/each}
</div>

<!-- No Results Message -->
{#if filteredEvents.length === 0}
	<div class="text-center py-12">
		<div class="text-white/60 text-lg mb-2">
			<ion-icon name="search-outline" class="text-3xl"></ion-icon>
		</div>
		<p class="text-white/60 text-lg">No events found matching "{searchTerm}"</p>
		<p class="text-white/40 text-sm mt-2">Try adjusting your search terms</p>
	</div>
{/if}
