<script lang="ts">
	import { onNavigate } from '$app/navigation';
	import { base } from '$app/paths';
	import { page } from '$app/state';
	import '../app.postcss';

	// Reactive values with runes
	let isLoaded = $state(false);
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

	// Effect with runes
	$effect(() => {
		setTimeout(() => {
			isLoaded = true;
		}, 1000);
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
	<!-- Loading screen -->
	<div
		class="pointer-events-none fixed inset-0 z-50 flex items-center justify-center bg-black transition-opacity duration-1000"
		class:opacity-0={isLoaded}
		class:opacity-100={!isLoaded}
	>
		<div class="relative flex h-48 w-48">
			<img
				src="/lib/assets/CMYK-PNG.png"
				alt="Star6nine Loading Logo"
				class="h-full w-full object-contain filter transition-all duration-1000"
				class:blur-none={isLoaded}
				class:blur-md={!isLoaded}
				class:scale-100={isLoaded}
				class:scale-90={!isLoaded}
			/>
			<div
				class="bg-primary-500 absolute right-0 bottom-0 left-0 h-1 origin-left transform transition-transform duration-700"
				style="transform: scaleX({isLoaded ? 1 : 0})"
			></div>
		</div>
	</div>

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
			<div
				class="mt-1 flex flex-col items-center justify-between justify-items-center md:flex-row md:justify-between"
			>
				<div class="mb-6 md:mb-0">
					<img src="/lib/assets/CMYK-PNG.png" alt="Star6nine Footer Logo" class="h-8" />
				</div>
				<div class="flex space-x-6">
					<!-- Instagram -->
					<a
						href="https://www.instagram.com/star6.nine/"
						class="hover:text-primary-400 text-white transition-colors"
						aria-label="Instagram"
						target="_blank"
						rel="noopener noreferrer"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 24 24"
							fill="currentColor"
						>
							<path
								d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"
							/>
						</svg>
					</a>

					<!-- YouTube -->
					<a
						href="https://www.youtube.com/channel/UCxhkgu9roj4LMOJNgzNrMpQ"
						class="hover:text-primary-400 text-white transition-colors"
						aria-label="YouTube"
						target="_blank"
						rel="noopener noreferrer"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 24 24"
							fill="currentColor"
						>
							<path
								d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"
							/>
						</svg>
					</a>

					<!-- Spotify -->
					<a
						href="https://open.spotify.com/artist/4PHiEApmqAZgGyCvaJopFb?si=SiCBrCAqSceIw8feccC2hA"
						class="hover:text-primary-400 text-white transition-colors"
						aria-label="Spotify"
						target="_blank"
						rel="noopener noreferrer"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 24 24"
							fill="currentColor"
						>
							<path
								d="M12 0C5.4 0 0 5.4 0 12s5.4 12 12 12 12-5.4 12-12S18.66 0 12 0zm5.521 17.34c-.24.359-.66.48-1.021.24-2.82-1.74-6.36-2.101-10.561-1.141-.418.122-.779-.179-.899-.539-.12-.421.18-.78.54-.9 4.56-1.021 8.52-.6 11.64 1.32.42.18.479.659.301 1.02zm1.44-3.3c-.301.42-.841.6-1.262.3-3.239-1.98-8.159-2.58-11.939-1.38-.479.12-1.02-.12-1.14-.6-.12-.48.12-1.021.6-1.141C9.6 9.9 15 10.561 18.72 12.84c.361.181.481.78.241 1.2zm.120-3.36C15.24 8.4 8.82 8.16 5.16 9.301c-.6.179-1.2-.181-1.38-.721-.18-.601.18-1.2.72-1.381 4.26-1.26 11.28-1.02 15.721 1.621.539.3.719 1.02.419 1.56-.299.421-1.02.599-1.559.3z"
							/>
						</svg>
					</a>

					<!-- SoundCloud -->
					<a
						href="https://soundcloud.com/starsixty_nine"
						class="hover:text-primary-400 text-white transition-colors"
						aria-label="SoundCloud"
						target="_blank"
						rel="noopener noreferrer"
					>
						<svg
							width="24px"
							height="24px"
							viewBox="0 0 17 17"
							class="h-7 w-7"
							version="1.1"
							xmlns="http://www.w3.org/2000/svg"
							xmlns:xlink="http://www.w3.org/1999/xlink"
							fill="#000000"
						>
							<g id="SVGRepo_bgCarrier" stroke-width="0"></g>
							<g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
							<g id="SVGRepo_iconCarrier">
								<path
									d="M0.882 10.132l-0.139 0.875c-0.007 0.035-0.027 0.062-0.062 0.062s-0.056-0.027-0.062-0.062l-0.119-0.875 0.118-0.889c0.007-0.035 0.028-0.062 0.062-0.062s0.055 0.027 0.062 0.062l0.14 0.889zM1.521 10.132l-0.18 1.409c-0.007 0.035-0.035 0.062-0.069 0.062-0.035 0-0.062-0.027-0.062-0.068l-0.16-1.403c0.16-1.438 0.16-1.438 0.16-1.438 0-0.034 0.027-0.062 0.062-0.062 0.034 0 0.062 0.028 0.069 0.062l0.18 1.438zM2.153 10.132l-0.173 1.646c0 0.041-0.035 0.076-0.077 0.076s-0.076-0.035-0.083-0.076l-0.146-1.646 0.146-1.701c0.007-0.049 0.042-0.083 0.083-0.083 0.042 0 0.077 0.034 0.077 0.083l0.173 1.701zM2.792 10.132l-0.16 1.694c-0.007 0.056-0.048 0.091-0.097 0.091-0.048 0-0.090-0.035-0.090-0.091l-0.146-1.694 0.146-1.75c0-0.056 0.042-0.090 0.090-0.090 0.049 0 0.090 0.034 0.097 0.090l0.16 1.75zM3.431 10.132l-0.146 1.709c-0.007 0.062-0.056 0.111-0.111 0.111s-0.104-0.049-0.104-0.111l-0.139-1.709 0.139-1.624c0-0.057 0.049-0.105 0.104-0.105 0.056 0 0.104 0.049 0.111 0.105l0.146 1.624zM4.083 10.132l-0.146 1.709c0 0.068-0.056 0.125-0.118 0.125-0.069 0-0.118-0.057-0.125-0.125l-0.125-1.709c0.125-2.64 0.125-2.64 0.125-2.64 0.008-0.068 0.056-0.124 0.125-0.124 0.062 0 0.118 0.056 0.118 0.124l0.146 2.64zM4.722 10.146l-0.132 1.695c0 0.076-0.063 0.131-0.132 0.131-0.076 0-0.131-0.055-0.139-0.131l-0.111-1.695c0.111-3.25 0.111-3.25 0.111-3.25 0.007-0.076 0.062-0.132 0.139-0.132 0.069 0 0.132 0.056 0.132 0.132l0.132 3.25zM5.396 10.132l-0.125 1.681c-0.007 0.083-0.069 0.146-0.153 0.146-0.076 0-0.139-0.062-0.146-0.146l-0.111-1.681 0.111-3.514c0-0.083 0.070-0.153 0.146-0.153 0.083 0 0.146 0.070 0.153 0.153l0.125 3.514zM6.056 10.132l-0.112-3.632c-0.006-0.090-0.076-0.167-0.166-0.167-0.083 0-0.16 0.077-0.16 0.167l-0.098 3.632 0.098 1.674c0.007 0.090 0.077 0.16 0.16 0.16 0.090 0 0.16-0.070 0.167-0.16l0.111-1.674zM6.722 10.132l-0.104 1.66c0 0.097-0.076 0.174-0.174 0.174-0.097 0-0.167-0.077-0.173-0.174l-0.098-1.66 0.098-3.542c0-0.098 0.076-0.174 0.173-0.174 0.098 0 0.174 0.076 0.174 0.174l0.104 3.542zM7.403 10.139l-0.098 1.64c0 0.104-0.083 0.188-0.187 0.188s-0.188-0.084-0.194-0.188l-0.083-1.64 0.083-3.416c0.007-0.111 0.090-0.195 0.194-0.195 0.104 0 0.18 0.084 0.187 0.195l0.098 3.416zM8.076 10.139l-0.083-4.070c0-0.069-0.035-0.132-0.090-0.166-0.035-0.021-0.070-0.035-0.111-0.035-0.042 0-0.076 0.014-0.111 0.035-0.056 0.035-0.091 0.097-0.091 0.166l-0.007 0.041-0.070 4.021c0 0 0 0.007 0.077 1.639 0 0 0 0 0 0.008 0 0.041 0.014 0.083 0.042 0.117 0.042 0.049 0.097 0.076 0.16 0.076 0.056 0 0.104-0.027 0.139-0.062 0.042-0.034 0.062-0.083 0.062-0.139l0.007-0.166 0.076-1.465zM8.681 11.743c0 0.118-0.097 0.215-0.215 0.215s-0.215-0.097-0.223-0.215l-0.041-0.791-0.042-0.813 0.083-4.416v-0.022c0.007-0.062 0.035-0.125 0.084-0.166 0.034-0.027 0.083-0.049 0.138-0.049 0.035 0 0.077 0.014 0.104 0.035 0.062 0.034 0.104 0.104 0.111 0.18l0.097 4.438-0.096 1.604zM14.535 11.966c-5.452 0-5.458 0-5.458 0-0.118-0.014-0.215-0.104-0.215-0.229v-6.245c0-0.117 0.042-0.173 0.195-0.229 0.382-0.152 0.812-0.235 1.257-0.235 1.812 0 3.299 1.388 3.458 3.159 0.236-0.097 0.493-0.153 0.764-0.153 1.083 0 1.965 0.883 1.965 1.973-0.001 1.084-0.883 1.959-1.966 1.959z"
									fill="#ffffff"
								></path>
							</g>
						</svg>
					</a>

					<!-- Linktree -->
					<a
						href="https://linktr.ee/ybrthelabel"
						class="hover:text-primary-400 text-white transition-colors"
						aria-label="Linktree"
						target="_blank"
						rel="noopener noreferrer"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 417 512.238"
							fill="currentColor"
							class="h-6 w-6"
						>
							<path
								d="M171.274 344.942h74.09v167.296h-74.09V344.942zM0 173.468h126.068l-89.622-85.44 49.591-50.985 85.439 87.829V0h74.086v124.872L331 37.243l49.552 50.785-89.58 85.24H417v70.502H290.252l90.183 87.629L331 381.192 208.519 258.11 86.037 381.192l-49.591-49.591 90.218-87.631H0v-70.502z"
							/>
						</svg>
					</a>
				</div>
			</div>
			<div class="text-surface-300 mt-1 text-center text-sm">
				© {new Date().getFullYear()} Star6nine. All rights reserved.
			</div>
		</div>
	</footer>
</div>
