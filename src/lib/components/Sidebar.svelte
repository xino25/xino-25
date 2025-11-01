<script>
    import { fly } from 'svelte/transition';
    import { onMount, onDestroy } from 'svelte';

    const cryptbg = '/assets/logos/crypt_bg.png';
    const athenaLogo = '/assets/sponsors/athena.png';
    const prodotLogo = '/assets/sponsors/prodot.png';
    const xyzLogo = '/assets/sponsors/xyz.png';

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
        }, 5000); // 10 seconds
    });

    onDestroy(() => {
        if (autoScrollInterval) {
            clearInterval(autoScrollInterval);
        }
    });

</script>



<aside class="hidden lg:fixed right-0 top-0 h-screen w-80 p-4 z-10 lg:flex flex-col gap-4 overflow-hidden">
	<!-- Sponsors -->
	<div class="bg-blur p-6 flex-5 max-h-2/5">
		<div class="text-center h-full">
			<p class="text-sm text-white/60 uppercase tracking-wider mb-4">In Collaboration With</p>
			
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
								<div class="w-3/4 aspect-square mb-2 flex items-center justify-center">
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
									class="px-6 py-2 bg-white/10 hover:bg-white/20 rounded-full text-white/75 text-sm transition-all duration-200 hover:scale-105"
								>
									Learn more
								</a>
							</div>
						{/key}
					</div>
				</div>
			</div>

			<!-- Dots Indicator -->
			<div class="flex justify-center gap-2 mt-4">
				{#each sponsors as _, index}
					<button
						on:click={() => goToSponsor(index)}
						aria-label="Go to sponsor {index + 1}"
						class="w-2 h-2 rounded-full transition-all duration-200 cursor-pointer {index === currentSponsorIndex ? 'bg-green-400' : 'bg-white/30'}"
					></button>
				{/each}
			</div>
		</div>
	</div>

	<!-- Section 2 -->
	<div class="bg-blur p-6 flex-3 flex flex-col justify-center">
		<p class="text-center">
            <span class="font-xirod text-white/90 text-4xl ">
                XINO <span class="text-green-700">'25</span>
            </span>
            <!-- <span class="text-xl text-white/80">
                With <span class="font-bold">AutoMeta</span>
            </span> -->
        </p>
        <span class="text-md text-white/60 block text-center mt-2">
             13th November 2025
        </span>

        <div class="flex mx-auto items-center justify-center mt-1">
            <!-- download borchure -->
            <!-- svelte-ignore a11y_consider_explicit_label -->
            <a 
                href="/brochure.pdf"  
                target="_blank"
                class="mt-4 px-4 py-2 text-white rounded-full  transition-all duration-200 hover:scale-105 hover:bg-white/20 bg-white/10 text-bold text-xl"
            >
                <ion-icon name="download-outline"></ion-icon>
            </a>


            <!-- register -->
                <a 
                href="/register"  
                target="_blank"
                class="mt-4 ml-4 px-4 py-2 bg-white/10 hover:bg-white/20 rounded-full text-white text-sm transition-all duration-200 hover:scale-105"
            >
                Register Now
            </a>
            
        </div>

	</div>

	<!-- Section 3 -->
	<div class="flex-3 relative overflow-hidden bg-blur">
		<!-- Crypt background with overlay -->
		<div 
			class="absolute inset-0 bg-cover bg-center opacity-75"
			style="background-image: url({cryptbg}); filter: brightness(0.9) contrast(1.1);"
		></div>

		
		<!-- Content area (ready for future content) -->
		<div class="relative z-10 p-4 h-full flex flex-col items-center justify-around">
			<div class="flex flex-col items-center justify-center">
                <span class="font-xirod text-4xl text-white/90">
                                XCRYPT
                            </span>
                            <span class="text-sm text-white/75 block text-center mt-2   ">
                                6th November - 7th November
                            </span>
            </div>

            <div class="flex items-center justify-center">
             
            <a 
                href="/xcryptreg"  
                target="_blank"
                class="mt-4 ml-4 px-4 py-2 bg-white/20   hover:bg-white/30 rounded-full text-white text-sm transition-all duration-200 hover:scale-105"
            >
                Register
            </a>
            <a 
                href="https://xcrypt.xino.in"  
                target="_blank"
                class="mt-4 ml-4 px-4 py-2 bg-white/20 hover:bg-white/30 rounded-full text-white text-sm transition-all duration-200 hover:scale-105"
            >
                Website
            </a>
            </div>




		</div>
	</div>
</aside>