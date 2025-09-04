<script lang="ts">
	import { onNavigate } from '$app/navigation';
	import { base } from '$app/paths';
	import { page } from '$app/state';
	import '../app.postcss';

	// Reactive values with runes
	let isNavigating = $state(false);
	let isMobileMenuOpen = $state(false);

	let { children } = $props();

	// Handle navigation animations with runes
	onNavigate(({ from, to }) => {
		if (!from || !to) return;

		isNavigating = true;

		return () => {
			setTimeout(() => {
				isNavigating = false;
			}, 500);
		};
	});

	// Navigation items - only Home and EPK
	const navItems = [
		{ name: 'Home', path: '/' },
		{ name: 'EPK', path: '/epk' }
	];
</script>

<svelte:head>
	<title>Star6nine | Official Website</title>
	<meta
		name="description"
		content="Official website of Star6nine - Dubstep Producer & DJ - Music, EPK & More"
	/>
	<meta property="og:title" content="Star6nine | Official Website" />
	<meta
		property="og:description"
		content="Official website of Star6nine - Dubstep Producer & DJ - Music, EPK & More"
	/>
	<meta property="og:type" content="website" />
	<meta property="og:url" content="https://star6nine.space" />
	<meta property="og:image" content="https://star6nine.space/lib/assets/star6ninelogo.png" />
	<meta name="twitter:card" content="summary_large_image" />
	<link rel="canonical" href="https://star6nine.space{page.url.pathname}" />
</svelte:head>

<div class="app bg-surface-900 flex min-h-screen flex-col overflow-hidden text-white">
	<!-- Header -->
	<header
		class="bg-surface-900/80 border-surface-700/50 fixed top-0 z-40 w-full border-b backdrop-blur-md transition-all duration-300"
		class:py-4={page.url.pathname === '/'}
		class:py-3={page.url.pathname !== '/'}
	>
		<div class="container mx-auto flex items-center justify-between px-4">
			<!-- Logo -->
			<a href="{base}/" class="relative z-10 flex items-center">
				<img src="/lib/assets/CMYK-PNG.png" alt="Star6nine Header Logo" class="h-8" />
			</a>

			<!-- Navigation -->
			<nav class="hidden space-x-8 md:flex">
				{#each navItems as item}
					<a
						href="{base}{item.path}"
						class="hover:text-primary-400 relative py-2 text-lg tracking-wider uppercase transition-colors"
						class:font-bold={page.url.pathname === item.path}
						class:text-primary-400={page.url.pathname === item.path}
						class:text-white={page.url.pathname !== item.path}
					>
						{item.name}
						{#if page.url.pathname === item.path}
							<span
								class="bg-primary-400 absolute bottom-0 left-0 h-0.5 w-full origin-left transform"
							></span>
						{/if}
					</a>
				{/each}
			</nav>

			<!-- Mobile menu button -->
			<button
				class="p-2 md:hidden"
				aria-label="Toggle menu"
				onclick={() => (isMobileMenuOpen = true)}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke="currentColor"
					class="h-6 w-6"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M4 6h16M4 12h16M4 18h16"
					></path>
				</svg>
			</button>
		</div>
	</header>

	<!-- Mobile menu - using conditional rendering instead of transforms -->
	{#if isMobileMenuOpen}
		<div class="fixed inset-0 z-40 bg-black">
			<div class="container mx-auto flex h-full flex-col px-4 py-12">
				<div class="flex justify-end">
					<button class="p-2" aria-label="Close menu" onclick={() => (isMobileMenuOpen = false)}>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke="currentColor"
							class="h-6 w-6"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M6 18L18 6M6 6l12 12"
							></path>
						</svg>
					</button>
				</div>

				<nav class="flex flex-1 flex-col items-center space-y-6">
					<!-- Logo as the first navigation item -->
					<div class="flex flex-col items-center mt-40 mb-20">
						<img src="/lib/assets/CMYK-PNG.png" alt="Star6nine Logo" class="mb-2 h-16" />
					</div>

					{#each navItems as item}
						<a
							href="{base}{item.path}"
							class="hover:text-primary-400 text-2xl tracking-widest uppercase transition-colors"
							class:font-bold={page.url.pathname === item.path}
							class:text-primary-400={page.url.pathname === item.path}
							onclick={() => (isMobileMenuOpen = false)}
						>
							{item.name}
						</a>
					{/each}
				</nav>
			</div>
		</div>
	{/if}

	<!-- Page transitions -->
	<main
		class="flex-1 pt-12 transition-opacity duration-150 md:px-[6rem]"
		class:opacity-0={isNavigating}
		class:opacity-100={!isNavigating}
	>
		{@render children()}
	</main>

<!-- Footer -->
<footer class="bg-surface-800/80 border-surface-700/50 border-t py-2">
	<div class="container mx-auto px-4">
		<div class="flex justify-center items-center md:justify-start">
			<div class="mt-4 flex items-center">
				<img src="/lib/assets/CMYK-PNG.png" alt="Star6nine Footer Logo" class="h-8" />
			</div>
		</div>
		<div class="text-surface-300 mt-1 text-center text-sm">
			© {new Date().getFullYear()} Star6nine. All rights reserved.
		</div>
	</div>
</footer>
</div>
