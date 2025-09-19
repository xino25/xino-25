<script>
	import { page } from '$app/stores';
	
	// Import navigation icons
	import homeIcon from '$lib/assets/nav/home.png';
	import calenderIcon from '$lib/assets/nav/calender.png';
	import membersIcon from '$lib/assets/nav/members.png';
	import otherIcon from '$lib/assets/nav/other.png';

	const navItems = [
		{ href: '/', label: 'Home', icon: homeIcon },
		{ href: '/members', label: 'Members', icon: membersIcon },
		{ href: '/events', label: 'Events', icon: calenderIcon },
		{ href: '/info', label: 'Info', icon: otherIcon }
	];
</script>

<nav class="fixed top-4 left-4 h-[calc(100vh-2rem)] w-24 bg-white/10 backdrop-blur-lg rounded-2xl shadow-xl z-50">
	<div class="flex flex-col h-full p-6">

		<!-- Navigation Links -->
		<ul class="flex flex-col justify-evenly h-full">
			{#each navItems as item}
				<li>
					<a
						href={item.href}
						class="flex items-center justify-center p-3 rounded-xl transition-all duration-200 group
							{$page.url.pathname === item.href
								? 'bg-white/20 text-white shadow-lg'
								: 'text-white/80 hover:bg-white/10 hover:text-white'
							}"
					>
						<img 
							src={item.icon} 
							alt={item.label}
							class="w-6 h-6 group-hover:scale-120 transition-transform duration-200 filter brightness-0 invert "
						/>
					</a>
				</li>
			{/each}
		</ul>

	</div>
</nav>