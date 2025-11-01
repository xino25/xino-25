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
			description: "Classic event converging entrepreneurship, development, and design. Conceptualize and pitch a product with working prototype, UI/UX, 2D/3D designs, and A/V submission",
			type: "Creative",
			keywords: ["creative", "entrepreneurship", "product", "prototype", "UI/UX", "design", "development", "presentation", "hackathon"]
		},
		
		// Discussion Events
		{
			name: "Xclamation Point!",
			description: "Colossal clash of ideas and opinions through group discussion. Present arguments with clarity, structure, and originality via video submissions",
			type: "Discussion",
			keywords: ["group discussion", "debate", "ideas", "opinions", "arguments", "speech", "video submission", "innovation"]
		},
		
		// Programming Events
		{
			name: "eXecute.eXe",
			description: "Test your programming skills and algorithmic knowledge. Heated competitive programming clash on Hackerrank judged on efficiency and speed",
			type: "Programming",
			keywords: ["competitive programming", "algorithms", "hackerrank", "coding", "DSA", "efficiency", "logic", "cp"]
		},
		
		// Surprise Events
		{
			name: "Xclusive",
			description: "Expect the unexpected! Mystery surprise event with online prelims determining 6 teams for offline finals",
			type: "Surprise",
			keywords: ["surprise", "mystery", "unexpected", "exclusive", "challenge", "prelims"]
		},
		
		// Quiz Events
		{
			name: "techXult Jr.",
			description: "Junior level technology quiz for grades VIII-X. Online prelims with top 6 teams advancing to offline finals",
			type: "Quiz",
			keywords: ["quiz", "junior", "technology", "VIII-X", "knowledge", "trivia", "prelims"]
		},
		{
			name: "techXult Sr.",
			description: "Senior level technology quiz for grades XI-XII. Online prelims with top 6 teams advancing to offline finals",
			type: "Quiz", 
			keywords: ["quiz", "senior", "technology", "XI-XII", "knowledge", "trivia", "prelims"]
		},
		
		// Cube Solving Events
		{
			name: "XCube 2x2",
			description: "Solve your way to victory! 2x2 Rubik's cube speed solving competition with online prelims and top 12 advancing to offline finals",
			type: "Cubing",
			keywords: ["cube", "2x2", "rubiks", "speed solving", "puzzle", "cubing", "competition"]
		},
		{
			name: "XCube 3x3",
			description: "Solve your way to victory! 3x3 Rubik's cube speed solving competition with online prelims and top 12 advancing to offline finals",
			type: "Cubing",
			keywords: ["cube", "3x3", "rubiks", "speed solving", "cubing", "puzzle", "competition"]
		},
		{
			name: "XCube Pyraminx",
			description: "Solve your way to victory! Pyraminx speed solving competition with online prelims and top 12 advancing to offline finals",
			type: "Cubing",
			keywords: ["cube", "pyraminx", "speed solving", "cubing", "puzzle", "competition"]
		},
		
		// Film Making Events
		{
			name: "XFrame",
			description: "Stories find their screen! Create films up to 5 minutes bringing imagination alive. Judged on creativity, relevance, and originality",
			type: "Film Making",
			keywords: ["film making", "video", "cinematography", "creativity", "storytelling", "originality", "short film"]
		},
		
		// Robotics Events
		{
			name: "autoTrack",
			description: "Build autonomous line follower bot to navigate tracks with speed and accuracy. ",
			type: "Robotics",
			keywords: ["robotics", "line follower", "autonomous", "bot", "engineering", "hardware", "automation", "speed"]
		},
		
		// Machine Learning Events
		{
			name: "autoCognito",
			description: "Build AI/ML-powered bot to master custom game. Train, tune, and optimize your model through logic and learning to outsmart opponents",
			type: "Machine Learning",
			keywords: ["machine learning", "AI", "artificial intelligence", "bot", "game", "training", "optimization", "strategy"]
		},
		
		// Cryptic Hunt Events
		{
			name: "XCrypt",
			description: "Dive into mystery, solve intricate puzzles, and prove your mettle. Unlock secrets and become the ultimate Cryptic Hunt champion",
			type: "Cryptic Hunt",
			keywords: ["cryptic", "hunt", "puzzles", "mystery", "clues", "solving", "secrets", "riddles"]
		},
		
		// Photography Events
		{
			name: "XPosure",
			description: "Capture stories in a single frame. Freeze imagination, emotion, and perspective through the lens with creative photography",
			type: "Photography",
			keywords: ["photography", "camera", "creative", "artistic", "visual", "composition", "storytelling", "imagery"]
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
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-12">
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
			<div class="relative p-6 h-56 flex flex-col justify-center">
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
