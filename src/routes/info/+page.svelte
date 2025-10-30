<svelte:head>
	<title>XINO | Info</title>
</svelte:head>

<script>
	
    import { fly } from 'svelte/transition';
	
    import { onMount, onDestroy } from 'svelte';

	const athenaLogo = '/assets/sponsors/athena.png';
	const prodotLogo = '/assets/sponsors/prodot.png';
	const xyzLogo = '/assets/sponsors/xyz.png';
	const cryptBg = '/assets/logos/crypt_bg.png';

	let copyFeedback = '';

	const contactInfo = [
		{ 
			label: "Email",
			info: "xino@dpsrohini.in", 
			href: "mailto:xino@dpsrohini.in",
			icon: "mail-outline"
		},
		{ 
			label: "Instagram",
			info: "@xino.dpsr", 
			href: "https://instagram.com/xino.dpsr",
			icon: "logo-instagram"
		},
		{ 
			label: "Discord",
			info: "Discord", 
			href: "/discord",
			icon: "logo-discord"
		}
	];

	const downloadsInfo = [
		{
			label: "BROCHURE - XINO25",
			href: "/brochure",
			icon: "cloud-download-outline"
		},
		{
			label: "Invite - XCrypt25", 
			href: "/xrcyptdc",
			icon: "cloud-download-outline"
		},
		{
			label: "X-Crypt discord",
			href: "/xrcyptdc",
			icon: "open-outline"
		}
	];

	const sponsors = [
        {
            name: "Athena Education",
            logo: athenaLogo,
            link: "https://www.athenaeducation.co.in/"
        },
        {
            name: "ProDot",
            logo: prodotLogo,
            link: "https://www.prodotgroup.com/"
        }
    ];

	async function copyToClipboard(text, label) {
		try {
			await navigator.clipboard.writeText(text);
			copyFeedback = `${label} copied!`;
			setTimeout(() => {
				copyFeedback = '';
			}, 2000);
		} catch (err) {
			console.error('Failed to copy: ', err);
			// Fallback for older browsers
			const textArea = document.createElement('textarea');
			textArea.value = text;
			document.body.appendChild(textArea);
			textArea.select();
			document.execCommand('copy');
			document.body.removeChild(textArea);
			copyFeedback = `${label} copied!`;
			setTimeout(() => {
				copyFeedback = '';
			}, 2000);
		}
	}

    let currentSponsorIndex = 0;
    let slideDirection = 0; // -1 for left, 1 for right, 0 for direct jump
    let autoScrollInterval;

    function nextSponsor() {
        slideDirection = 1;
        currentSponsorIndex = (currentSponsorIndex + 1) % sponsors.length;
    }

    function prevSponsor() {
        slideDirection = -1;
        currentSponsorIndex = (currentSponsorIndex - 1 + sponsors.length) % sponsors.length;
    }

    function goToSponsor(index) {
        slideDirection = index > currentSponsorIndex ? 1 : -1;
        currentSponsorIndex = index;
    }

    // Auto-scroll functionality
    onMount(() => {
        autoScrollInterval = setInterval(() => {
            nextSponsor();
        }, 10000); // 10 seconds
    });

    onDestroy(() => {
        if (autoScrollInterval) {
            clearInterval(autoScrollInterval);
        }
    });
	
</script>

<div class="relative overflow-hidden ">
	<!-- Header Section (Top Right) -->
	<!-- <header class="hidden lg:block absolute top-6 right-6 text-right z-10 ">
		<div class="">
			<h1 class="text-5xl font-bold text-white mb-2 font-xirod">
				XIN<span class="text-emerald-400">O</span>
			</h1>
			<p class="text-lg tracking-wider">
				ExtremeInnovation@2025
			</p>
		</div>
	</header> -->

	<!-- Main Content - Event Tiles (Centered Grid) -->
	<main class="flex flex-col items-center justify-center px-6 lg:pt-12 gap-10">
		<div class="flex flex-col lg:flex-row justify-around gap-8 max-w-7xl w-full">
			
			<!-- Left Card - XINO x AutoMeta 2025 -->
			<div class="bg-blur p-8 rounded-xl text-center w-full flex flex-col items-center justify-center">
				<h2 class="text-white text-3xl font-bold mb-4 font-xirod">
					XINO 2025
				</h2>
				<p class="text-white/80 text-xl mb-8">
					13th November 2025
				</p>
				<a class="bg-emerald-600 hover:bg-emerald-700 hover:scale-105 text-white px-6 py-3 rounded-full font-semibold transition-all duration-200 flex justify-center items-center" href="/register">
					Register
				</a>
		</div>

			<!-- Right Card - XCrypt 2025 -->
			<div class="relative rounded-xl overflow-hidden w-full">
				<!-- Background Image with Overlay -->
				<div class="absolute inset-0 bg-cover bg-center" style="background-image: url({cryptBg});">
					<div class="absolute inset-0 bg-black/20 backdrop-blur-[1px]"></div>
				</div>
				
				<!-- Content -->
				<div class="relative p-8 text-center">
					<h2 class="text-white text-3xl font-bold mb-4">
						XCrypt 2025
					</h2>
					<p class="text-white/80 text-lg mb-8">
						11:00AM, 6th November 2025 - 11:00PM, 7th November 2025
					</p>
					<div class="flex gap-4 justify-center">
						<a class="bg-emerald-600 hover:bg-emerald-700 hover:scale-105 text-white px-6 py-2 rounded-full font-semibold transition-all duration-200 flex justify-center items-center" href="/xcrypt">
							Register
						</a>
						<a class="border border-white/50 hover:border-white hover:scale-105 text-white px-6 py-2 rounded-4xl font-semibold transition-all duration-300 flex justify-center items-center" href="https://xcrypt.xino.in/">
							XCrypt Website
						</a>
					</div>
				</div>
			</div>
		</div>


		<div class="flex flex-col lg:flex-row justify-around gap-8 max-w-7xl w-full text-center">
			
			<!-- Contact Info Tile (Left) -->
			<div class="bg-blur p-6 rounded-xl flex-1 w-full py-12 relative">
				{#if copyFeedback}
					<div class="absolute top-2 right-2 bg-emerald-500 text-white px-3 py-1 rounded-md text-sm">
						{copyFeedback}
					</div>
				{/if}
				<div class="space-y-4 flex flex-col justify-around h-full">
					{#each contactInfo as contact}
						<div class="flex items-center justify-between gap-3 hover:bg-white/10 rounded-lg p-2 transition-colors">
							<a 
								href={contact.href}
								target={contact.href.startsWith('mailto:') ? '_self' : '_blank'}
								rel={contact.href.startsWith('mailto:') ? '' : 'noopener noreferrer'}
								class="flex items-center gap-3 flex-1 text-white no-underline"
							>
								<div class="text-xl text-emerald-400 flex items-center justify-center">
									<ion-icon name={contact.icon}></ion-icon>
								</div>
								<span>{contact.info}</span>
							</a>
							<button 
								class="text-emerald-400 hover:text-emerald-300 p-2 transition-colors"
								on:click={() => copyToClipboard(contact.info, contact.label)}
								aria-label={`Copy ${contact.label}`}
							>
								<ion-icon name="copy-outline"></ion-icon>
							</button>
						</div>
					{/each}
				</div>
			</div>

			<!-- Downloads Tile (Middle) -->
			<div class="bg-blur p-6 rounded-xl flex-1 w-full py-12">
				<div class="space-y-4 flex flex-col h-full justify-around">
					{#each downloadsInfo as download}
						<a 
							href={download.href}
							target="_blank"
							class="flex items-center gap-3 text-white no-underline hover:bg-white/10 rounded-lg px-2 py-4 transition-colors"
						>
							<div class="text-xl text-emerald-400 flex items-center justify-center px-2">
									<ion-icon name={download.icon}></ion-icon>
							</div>
							<span>{download.label}</span>
					</a>
					{/each}
				</div>
			</div>

			<!-- Sponsor Tile (Right) -->
			<div class="bg-blur p-6 flex-1 w-full aspect-[5/3] max-w-lg mx-auto ">
		<div class="text-center h-full">
			<p class="text-sm text-white/60 uppercase tracking-wider mb-2">In Collaboration With</p>
			
			<!-- Sponsor Carousel -->
			<div class="relative h-3/4">
				<!-- Navigation Arrows -->
				<button 
					on:click={prevSponsor}
					aria-label="Previous sponsor"
					class="absolute left-0 top-1/2 transform -translate-y-1/2 z-10 w-8 h-8 bg-green-700 hover:bg-green-800 rounded-full flex items-center justify-center transition-colors cursor-pointer"
				>
					<span class="text-white text-2xl font-bold text-center flex items-center justify-center">
                        <ion-icon name="chevron-back-outline"></ion-icon>
                    </span>
				</button>
				
				<button 
					on:click={nextSponsor}
					aria-label="Next sponsor"
					class="absolute right-0 top-1/2 transform -translate-y-1/2 z-10 w-8 h-8 bg-green-700 hover:bg-green-800 rounded-full flex items-center justify-center transition-colors cursor-pointer"
				>
					<span class="text-white text-2xl font-bold text-center flex items-center justify-center">
                        <ion-icon name="chevron-forward-outline"></ion-icon>
                    </span>
				</button>

				<!-- Sponsor Content -->
				<div class="mx-10 py-4 h-full relative">
					<div class="h-full relative">
						{#key currentSponsorIndex}
							<div 
								in:fly="{{ x: slideDirection * 200, duration: 300, delay: 0 }}"
								out:fly="{{ x: slideDirection * -200, duration: 300 }}"
								class="flex flex-col items-center justify-center h-full w-full"
								style="position: absolute; top: 0; left: 0; right: 0; bottom: 0;"
							>
								<!-- Logo -->
								<div class="w-1/2 aspect-square mb-2 flex items-center justify-center">
									<img 
										src={sponsors[currentSponsorIndex].logo} 
										alt={sponsors[currentSponsorIndex].name}
										class="max-w-full max-h-full object-contain"
									/>
								</div>

								
								<!-- Learn More Button -->
								<a 
									href={sponsors[currentSponsorIndex].link}
									target="_blank"
									rel="noopener noreferrer"
									class="px-3 xl:px-6 py-2 bg-white/10 hover:bg-white/20 rounded-full text-white/75 text-xs xl:text-sm transition-all duration-200 hover:scale-105"
								>
									Learn more
								</a>
							</div>
						{/key}
					</div>
				</div>
			</div>

			
		</div>
	</div>

		</div>
	</main>

	<!-- Bottom Section (3 Tiles in a Row) -->

</div>