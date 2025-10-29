<script>
	import { page } from '$app/stores';
	
	// Navigation icons from static folder
	const navItems = [
		{ href: '/', label: 'Home', icon: '/assets/nav/home.png' },
		{ href: '/members', label: 'Members', icon: '/assets/nav/members.png' },
		{ href: 'https://xcrypt.xino.in', label: 'Xcrypt', icon: '/assets/nav/logo.png' },
		{ href: '/events', label: 'Events', icon: '/assets/nav/calender.png' },
		{ href: '/info', label: 'Info', icon: '/assets/nav/other.png' }
	];
</script>

<!-- Desktop Sidebar (md and up) -->
<nav class="hidden lg:block fixed top-4 left-4 h-[calc(100vh-2rem)] w-24 bg-blur z-50">
	<div class="flex flex-col h-full p-4">
		<!-- Navigation Links -->
		<ul class="flex flex-col justify-evenly h-full">
			{#each navItems as item}
				<li>
					<a
						href={item.href}
						class="flex items-center justify-center p-3 rounded-xl transition-all duration-200 group relative
							{item.label === 'Xcrypt' 
								? 'w-16 py-6' 
								: $page.url.pathname === item.href
									? 'bg-white/20 text-white shadow-lg'
									: 'text-white/80 hover:bg-white/10 hover:text-white'
							}"
					>
						<img 
							src={item.icon} 
							alt={item.label}
							class="{item.label === 'Xcrypt' ? 'h-16 w-16 absolute' : 'w-8 h-8'} group-hover:scale-110 transition-transform duration-200 filter brightness-0 invert"
						/>
						
						{#if item.label === 'Xcrypt'}
							<span class="absolute top-full mt-2 px-2 py-1 text-xs font-medium rounded-md opacity-0 group-hover:opacity-100 transform translate-y-7 group-hover:translate-y-1 transition-all duration-300 whitespace-nowrap text-white/50">
								{item.label}
							</span>
						{/if}
					</a>
				</li>
			{/each}
		</ul>
	</div>
</nav>

<!-- Mobile Top Bar (below md) -->
<nav class="lg:hidden fixed top-4 left-4 right-4 h-16 bg-white/10 backdrop-blur-lg rounded-2xl shadow-xl z-50">
	<div class="flex items-center justify-between h-full px-6">
		<!-- Navigation Links -->
		<ul class="flex items-center justify-evenly w-full">
			{#each navItems as item}
				<li>
					<a
						href={item.href}
						class="flex items-center justify-center p-2 rounded-xl transition-all duration-200
							{item.label === 'Xcrypt' 
								? '' 
								: $page.url.pathname === item.href
									? 'bg-white/20 text-white shadow-lg'
									: 'text-white/80'
							}"
					>
						<img 
							src={item.icon} 
							alt={item.label}
							class="{item.label === 'Xcrypt' ? 'h-10 w-10' : 'w-6 h-6'} filter brightness-0 invert"
						/>
					</a>
				</li>
			{/each}
		</ul>
	</div>
</nav>