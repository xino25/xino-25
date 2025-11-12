<svelte:head>
	<title>XINO | Events</title>
</svelte:head>

<script>
	import { onMount } from 'svelte';
	import { fly, fade } from 'svelte/transition';
	
	// Events data structure
	const events = [
		// Creative Events
		{
			name: "Xquisite",
			description: "Classic event converging entrepreneurship, development, and design. Conceptualize and pitch a product with working prototype, UI/UX, 2D/3D designs, and A/V submission",
			type: "Creative",
			keywords: ["creative", "entrepreneurship", "product", "prototype", "UI/UX", "design", "development", "presentation", "hackathon"],
			eligibility: "IX-XII",
			teamSize: "4",
			fullDescription: "Xquisite is our flagship event that brings together entrepreneurship, development, and design. Teams must conceptualize and pitch an innovative product complete with a working prototype, UI/UX designs, 2D/3D models, and audio-visual presentation.",
			prelimsDetails: null,
			prelimsBrochureLink: "https://docs.google.com/document/d/1yl71rOPIOMnIlx790T-a-vtFFA1AlNiu9C6wWbyO0sw/edit?usp=sharing",
			prelimsResults: [
				"DPS Vasant Kunj",
				"DPS RK Puram",
				"The Mother's International School",
				"Bal Bharati School, Pitampura",
				"DPS Dwarka",
				"DPS Rohini"
			]
		},
		
		// Discussion Events
		{
			name: "Xclamation Point!",
			description: "Colossal clash of ideas and opinions through group discussion. Present arguments with clarity, structure, and originality via video submissions",
			type: "Discussion",
			keywords: ["group discussion", "debate", "ideas", "opinions", "arguments", "speech", "video submission", "innovation"],
			eligibility: "IX-XII",
			teamSize: "1",
			fullDescription: "A dynamic group discussion event where teams engage in intellectual debates on contemporary topics. Showcase your argumentative skills, critical thinking, and presentation abilities through structured video submissions.",
			prelimsDetails: null,
			prelimsBrochureLink: "https://docs.google.com/document/d/13ubWDg99Pe95ARQnxC3lpY0jROIunbozNVJaffYeWRM/edit?usp=sharing",
			prelimsResults: [
				"DPS RK Puram",
				"DPS Vasant Kunj",
				"DPS Noida",
				"DPS Sushant Lok",
				"The Mother's International School",
				"Bal Bharati School, Pitampura",
				"DPS Dwarka",
				"Ryan International School, Rohini",
				"DPS Rohini"
			]
		},
		
		// Programming Events
		{
			name: "eXecute.eXe",
			description: "Test your programming skills and algorithmic knowledge. Heated competitive programming clash on Hackerrank judged on efficiency and speed",
			type: "Programming",
			keywords: ["competitive programming", "algorithms", "hackerrank", "coding", "DSA", "efficiency", "logic", "cp"],
			eligibility: "VIII-XII",
			teamSize: "1",
			fullDescription: "Put your coding skills to the ultimate test in this competitive programming challenge. Solve complex algorithmic problems on HackerRank, where every second counts and efficiency matters.",
			prelimsDetails: "Prelims will be conducted online. Further details will be shared on the Discord server.",
			prelimsBrochureLink: null,
			prelimsResults: [
				"DPS RK Puram",
				"DPS Noida",
				"Mount Carmel School Dwarka",
				"DPS Dwarka",
				"Bal Bharti Public School Pitampura",
				"Ryan International School, Vasant Kunj",
				"The Mother's International School",
				"ORCHIDS The International School, Sonepat",
				"DPS Rohini"
			]
		},
		
		// Surprise Events
		{
			name: "Xclusive",
			description: "Expect the unexpected! Mystery surprise event with online prelims determining 6 teams for offline finals",
			type: "Surprise",
			keywords: ["surprise", "mystery", "unexpected", "exclusive", "challenge", "prelims"],
			eligibility: "IX-XII",
			teamSize: "2",
			fullDescription: "The ultimate mystery event where anything can happen! Details will be revealed closer to the event date. Prepare for the unexpected and showcase your versatility.",
			prelimsDetails: "Prelims will be conducted online. Further details will be shared on the Discord server.",
			prelimsBrochureLink: null,
			prelimsResults: [
				"DPS Dwarka",
				"DPS Sushant Lok",
				"DPS Noida",
				"DPS International Saket",
				"The Mother's International School",
				"DPS Vasant Kunj",
				"DPS Rohini",
				"DPS RK Puram"
			]
		},
		
		// Quiz Events
		{
			name: "techXult Jr.",
			description: "Junior level technology quiz for grades VIII-X. Online prelims with top 6 teams advancing to offline finals",
			type: "Quiz",
			keywords: ["quiz", "junior", "technology", "VIII-X", "knowledge", "trivia", "prelims"],
			eligibility: "VIII-X",
			teamSize: "2",
			fullDescription: "A comprehensive technology quiz designed for junior students. Test your knowledge across various domains of computer science, technology trends, and digital innovations.",
			prelimsDetails: "Prelims will be conducted online. Further details will be shared on the Discord server.",
			prelimsBrochureLink: null,
			prelimsResults: [
				"DPS RK Puram",
				"Mother's International",
				"DPS International",
				"DPS Noida",
				"DPS Rohini",
				"Ryan International, Sec25 Rohini"
			]
		},
		{
			name: "techXult Sr.",
			description: "Senior level technology quiz for grades XI-XII. Online prelims with top 6 teams advancing to offline finals",
			type: "Quiz", 
			keywords: ["quiz", "senior", "technology", "XI-XII", "knowledge", "trivia", "prelims"],
			eligibility: "XI-XII",
			teamSize: "2",
			fullDescription: "An advanced technology quiz for senior students covering in-depth topics in computer science, emerging technologies, programming concepts, and tech industry knowledge.",
			prelimsDetails: "Prelims will be conducted online. Further details will be shared on the Discord server.",
			prelimsBrochureLink: null,
			prelimsResults: [
				"DPS RK Puram",
				"Mother's International",
				"DPS International",
				"DPS Mathura Road",
				"DPS Rohini",
				"BBPS Pitampura"
			]
		},
		
		// Cube Solving Events
		{
			name: "XCube 2x2",
			description: "Solve your way to victory! 2x2 Rubik's cube speed solving competition with online prelims and top 12 advancing to offline finals",
			type: "Cubing",
			keywords: ["cube", "2x2", "rubiks", "speed solving", "puzzle", "cubing", "competition"],
			eligibility: "Open",
			teamSize: "1",
			fullDescription: "Speed cubing competition featuring the 2x2 Rubik's cube. Demonstrate your solving speed and technique in this individual competition.",
			prelimsDetails: "Prelims will be conducted online. Further details will be shared on the Discord server.",
			prelimsBrochureLink: null,
			prelimsResults: [
				"Ryan International Rohini",
				"DPS Vasant Kunj",
				"DPS Dwarka",
				"DPS Mathura Road",
				"DPS RK Puram",
				"DPS Noida",
				"DPSI Saket",
				"Ryan International Vasant Kunj",
				"DPS Rohini"
			]
		},
		{
			name: "XCube 3x3",
			description: "Solve your way to victory! 3x3 Rubik's cube speed solving competition with online prelims and top 12 advancing to offline finals",
			type: "Cubing",
			keywords: ["cube", "3x3", "rubiks", "speed solving", "cubing", "puzzle", "competition"],
			eligibility: "Open",
			teamSize: "1",
			fullDescription: "The classic 3x3 Rubik's cube speed solving competition. Show off your algorithms and finger tricks to secure the fastest times.",
			prelimsDetails: "Prelims will be conducted online. Further details will be shared on the Discord server.",
			prelimsBrochureLink: null,
			prelimsResults: [
				"Ryan International Vasant Kunj",
				"Mothers International",
				"Ryan International Rohini",
				"DPS Vasant Kunj",
				"DPS Noida",
				"DPSI Saket",
				"DPS Mathura Road",
				"DPS RK Puram",
				"DPS Rohini"
			]
		},
		{
			name: "XCube Pyraminx",
			description: "Solve your way to victory! Pyraminx speed solving competition with online prelims and top 12 advancing to offline finals",
			type: "Cubing",
			keywords: ["cube", "pyraminx", "speed solving", "cubing", "puzzle", "competition"],
			eligibility: "Open",
			teamSize: "1",
			fullDescription: "Pyraminx speed solving competition. Master this unique triangular puzzle and compete for the best times.",
			prelimsDetails: "Prelims will be conducted online. Further details will be shared on the Discord server.",
			prelimsBrochureLink: null,
			prelimsResults: [
				"Ryan International Rohini",
				"DPSI Saket",
				"DPS RK Puram",
				"DPS Noida",
				"DPS Vasant Kunj",
				"DPS Mathura Road",
				"DPS Dwarka",
				"DPS Rohini"
			]
		},
		
		// Film Making Events
		{
			name: "XFrame",
			description: "Stories find their screen! Create films up to 5 minutes bringing imagination alive. Judged on creativity, relevance, and originality",
			type: "Film Making",
			keywords: ["film making", "video", "cinematography", "creativity", "storytelling", "originality", "short film"],
			eligibility: "IX-XII",
			teamSize: "4",
			fullDescription: "Unleash your creativity through the art of filmmaking. Create a compelling short film that tells a story, evokes emotions, and showcases your cinematographic skills.",
			prelimsDetails: "The suspense is over! We were truly blown away by the creative interpretations submitted in Xframe! The results are in, and we're thrilled to announce the winning teams.",
			prelimsBrochureLink: "https://docs.google.com/document/d/10QOLoxOYT6ro4k2GGuhZ-sKLn7aXYiM4XrNjhbSsM_0/edit?usp=sharing",
			prelimsResults: [
				"DPS Hyderabad (1st Place)",
				"St Marks, Meera Bagh (2nd Place)",
				"DPS Sushant Lok (3rd Place)"
			]
		},
		
		// Robotics Events
		{
			name: "autoTrack",
			description: "Build autonomous line follower bot to navigate tracks with speed and accuracy. ",
			type: "Robotics",
			keywords: ["robotics", "line follower", "autonomous", "bot", "engineering", "hardware", "automation", "speed"],
			eligibility: "VIII-XII",
			teamSize: "2",
			fullDescription: "Design and build an autonomous line-following robot that can navigate complex tracks with precision and speed. Test your engineering and programming skills in robotics.",
			prelimsDetails: "There are no prelims for this event. The final will be held offline on 13 November 2025.",
			prelimsBrochureLink: null
		},
		
		// Machine Learning Events
		{
			name: "autoCognito",
			description: "Build AI/ML-powered bot to master custom game. Train, tune, and optimize your model through logic and learning to outsmart opponents",
			type: "Machine Learning",
			keywords: ["machine learning", "AI", "artificial intelligence", "bot", "game", "training", "optimization", "strategy"],
			eligibility: "VIII-XII",
			teamSize: "2",
			fullDescription: "Create an AI-powered bot that learns and adapts to master a custom game. Apply machine learning algorithms, train your model, and compete against other AI bots.",
			prelimsDetails: null,
			prelimsBrochureLink: "https://docs.google.com/document/d/1xLShmt-0yh5ORyRwMUaAfzb-_jxr7RcE7aRcKvKlZWw/edit?usp=sharing"
		},
		
		// Cryptic Hunt Events
		{
			name: "XCrypt",
			description: "Dive into mystery, solve intricate puzzles, and prove your mettle. Unlock secrets and become the ultimate Cryptic Hunt champion",
			type: "Cryptic Hunt",
			keywords: ["cryptic", "hunt", "puzzles", "mystery", "clues", "solving", "secrets", "riddles"],
			eligibility: "Open",
			teamSize: "1",
			fullDescription: "Embark on an thrilling journey through cryptic puzzles, hidden clues, and mind-bending challenges. Use logic, creativity, and teamwork to unlock secrets and progress through levels.",
			prelimsDetails: "",
			prelimsBrochureLink: null,
			prelimsResults: [
				"DPS Vasant Kunj (1st Place)",
				"DPS RK Puram (2nd Place)",
				"DPS Sushant Lok (3rd Place)"
			]
		},
		
		// Photography Events
		{
			name: "XPosure",
			description: "Capture stories in a single frame. Freeze imagination, emotion, and perspective through the lens with creative photography",
			type: "Photography",
			keywords: ["photography", "camera", "creative", "artistic", "visual", "composition", "storytelling", "imagery"],
			eligibility: "IX-XII",
			teamSize: "2",
			fullDescription: "Express your artistic vision through photography. Capture compelling images that tell stories, evoke emotions, and showcase your unique perspective.",
			prelimsDetails: "The suspense is over! We were truly blown away by the creative interpretations submitted in the Preliminary Round of XPosure. The results are in, and we're thrilled to announce the photographers moving on to the final round on Thursday, 13 November 2025.",
			prelimsBrochureLink: "https://docs.google.com/document/d/1nPjMhMUXQNoXFsoOyINFdGk_etv9vigrnWBFryST5P8/edit?usp=sharing",
			prelimsResults: [
				"DPS RK Puram",
				"Ryan International, Rohini-25",
				"DPS Dwarka",
				"St Marks, Meera Bagh",
				"DPS Noida, S-30",
				"DPS Rohini"
			]
		}
	];

	// Search functionality
	let searchTerm = '';
	let filteredEvents = events;
	let searchPlaceholder = 'Search events by name, type, or keywords...';
	
	// Modal state
	let selectedEvent = null;
	let showModal = false;
	
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
	
	// Modal functions
	function openModal(event) {
		selectedEvent = event;
		showModal = true;
		// Prevent body scroll when modal is open
		document.body.style.overflow = 'hidden';
	}
	
	function closeModal() {
		showModal = false;
		selectedEvent = null;
		// Restore body scroll
		document.body.style.overflow = 'auto';
	}
	
	// Close modal on escape key
	function handleKeydown(e) {
		if (e.key === 'Escape' && showModal) {
			closeModal();
		}
	}
</script>

<svelte:window on:keydown={handleKeydown} />

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
			on:click={() => openModal(event)}
			on:keydown={(e) => e.key === 'Enter' && openModal(event)}
			role="button"
			tabindex="0"
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

<!-- Event Details Modal -->
{#if showModal && selectedEvent}
	<div 
		class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/70 backdrop-blur-sm"
		transition:fade="{{ duration: 200 }}"
		on:click={closeModal}
		on:keydown={(e) => e.key === 'Enter' && closeModal()}
		role="button"
		tabindex="0"
	>
		<div 
			class="bg-gradient-to-br from-gray-900 to-gray-800 rounded-2xl max-w-2xl w-full max-h-[90vh] overflow-y-auto border border-white/10 shadow-2xl"
			on:click|stopPropagation
			on:keydown|stopPropagation
			role="dialog"
			aria-modal="true"
			tabindex="-1"
			transition:fly="{{ y: 50, duration: 300 }}"
		>
			<!-- Modal Header -->
			<div class="sticky top-0 bg-gradient-to-br from-gray-900 to-gray-800 p-6 rounded-t-2xl">
				<div class="flex justify-between items-start">
					<div>
						<h2 class="text-white text-3xl font-bold mb-2">{selectedEvent.name}</h2>
						<span class="bg-white/20 text-white px-3 py-1 rounded-full text-sm">
							{selectedEvent.type}
						</span>
					</div>
					<button 
						on:click={closeModal}
						class="text-white/80 hover:text-white transition-colors p-2 hover:bg-white/10 rounded-lg"
						aria-label="Close modal"
					>
						<ion-icon name="close-outline" class="text-3xl"></ion-icon>
					</button>
				</div>
			</div>
			
			<!-- Modal Content -->
			<div class="p-4 space-y-6">
				<!-- Description -->
				<div>
					<p class="text-white/80 leading-relaxed">
						{selectedEvent.fullDescription}
					</p>
				</div>
				
				<!-- Eligibility -->
				<div>
					<p class="text-white/80">
						Classes: <span class="text-white font-semibold">{selectedEvent.eligibility}</span>
					</p>
				</div>
				
				<!-- Team Size -->
				<div>
					<p class="text-white/80">
						{selectedEvent.teamSize} {selectedEvent.teamSize === "1" ? "participant" : "participants"}
					</p>
				</div>
				
				<!-- Prelims Details -->
				<div>
					<h3 class="text-emerald-400 text-lg font-semibold mb-2 flex items-center gap-2">
						<ion-icon name="trophy-outline"></ion-icon>
						Preliminary Round Details
					</h3>
					{#if selectedEvent.prelimsBrochureLink}
						<a 
							href={selectedEvent.prelimsBrochureLink}
							target="_blank"
							rel="noopener noreferrer"
							class="inline-flex items-center gap-2 bg-emerald-600 hover:bg-emerald-500 text-white px-4 py-2 rounded-lg transition-colors duration-200"
						>
							<ion-icon name="document-text-outline"></ion-icon>
							View Event Prompt
							<ion-icon name="open-outline" class="text-sm"></ion-icon>
						</a>
					{:else if selectedEvent.prelimsDetails}
						<p class="text-white/80 leading-relaxed">
							{selectedEvent.prelimsDetails}
						</p>
					{/if}
				</div>
				
				<!-- Prelims Results -->
				{#if selectedEvent.prelimsResults && selectedEvent.prelimsResults.length > 0}
				<div>
					<h3 class="text-emerald-400 text-lg font-semibold mb-3 flex items-center gap-2">
						<ion-icon name="ribbon-outline"></ion-icon>
						{#if selectedEvent.name === "XCrypt" || selectedEvent.name === "XFrame"}
							Winners
						{:else}
							Qualified Teams
						{/if}
					</h3>
					{#if selectedEvent.name !== "XCrypt" && selectedEvent.name !== "XFrame"}
						<p class="text-white/60 text-sm mb-3 italic">In no particular order</p>
					{/if}
					<div class="bg-white/5 rounded-lg p-4 border border-emerald-500/20">
						<ul class="space-y-2">
							{#each selectedEvent.prelimsResults as school, index}
								<li class="flex items-center gap-3 text-white/90">
									{#if selectedEvent.name === "XCrypt" || selectedEvent.name === "XFrame"}
										<span class="flex-shrink-0 w-6 h-6 bg-emerald-600/30 rounded-full flex items-center justify-center text-emerald-300 text-sm font-semibold">
											{index + 1}
										</span>
									{:else}
										<span class="flex-shrink-0 w-2 h-2 bg-emerald-500 rounded-full"></span>
									{/if}
									<span>{school}</span>
								</li>
							{/each}
						</ul>
					</div>
				</div>
				{/if}
				
			</div>
		</div>
	</div>
{/if}
