<script lang="ts">
	import { Users, Music, FileText, Calendar, MapPin, Camera } from 'lucide-svelte';
	import { IconBrandSpotify, IconCloud } from '@tabler/icons-svelte';
	import { onMount } from 'svelte';

	let galleryVisible = false;
	let heroVisible = false;

	onMount(() => {
		// Stagger animations
		setTimeout(() => {
			heroVisible = true;
		}, 300);
		setTimeout(() => {
			galleryVisible = true;
		}, 800);
	});
</script>

<svelte:head>
	<title>Star6nine - Electronic Press Kit | Dubstep Producer & DJ</title>
	<meta
		name="description"
		content="Official Electronic Press Kit for Star6nine - Professional dubstep producer and DJ. Biography, performances, music, and press materials."
	/>
	<meta
		name="keywords"
		content="Star6nine, dubstep, electronic music, DJ, producer, press kit, EPK, Adam Vacha, bass music"
	/>
	<meta property="og:title" content="Star6nine - Electronic Press Kit" />
	<meta
		property="og:description"
		content="Official EPK for Star6nine - Dubstep Producer & DJ featuring biography, performances, and music"
	/>
	<meta property="og:type" content="profile" />
	<meta property="og:url" content="https://star6nine.space/epk" />
	<meta property="og:image" content="https://star6nine.space/lib/assets/star6ninelogo.png" />
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:title" content="Star6nine - Electronic Press Kit" />
	<meta name="twitter:description" content="Official EPK for Star6nine - Dubstep Producer & DJ" />
	<meta name="twitter:image" content="https://star6nine.space/lib/assets/star6ninelogo.png" />
	<link rel="canonical" href="https://star6nine.space/epk" />
</svelte:head>

<!-- HERO SECTION -->
<section class="h-auto sm:min-h-screen flex items-start sm:items-center justify-center overflow-hidden pt-20 sm:pt-0 mb-4 sm:mb-2">
	<div
		class="relative z-10 text-center max-w-4xl mx-auto px-6 transform transition-all duration-1000"
		class:translate-y-0={heroVisible}
		class:translate-y-8={!heroVisible}
		class:opacity-100={heroVisible}
		class:opacity-0={!heroVisible}
	>
		<!-- Logo -->
		<div class="mb-2">
			<img
				src="/lib/assets/star6ninelogo.png"
				alt="Star6nine Logo"
				class="w-full max-w-md mx-auto filter drop-shadow-2xl"
			/>
		</div>

		<!-- Video -->
		<div class="mb-2">
			<video
				class="w-full max-w-2xl mx-auto rounded-2xl shadow-2xl ring-1 ring-white/10"
				autoplay
				muted
				loop
				playsinline
			>
				<source src="/lib/assets/live/P101016969.webm" type="video/webm" />
				Your browser does not support the video tag.
			</video>
		</div>

		<!-- Title -->
		<h1
			class="text-3xl md:text-7xl font-bold bg-gradient-to-r from-white via-primary-200 to-primary-400 bg-clip-text mb-6"
		>
			Electronic Press Kit
		</h1>
		<p class="text-2xl md:text-3xl text-surface-300 font-light tracking-wide">
			Dubstep Producer & DJ
		</p>
	</div>
</section>

<!-- LIVE PERFORMANCE GALLERY -->
<section class="pt-8 sm:pt-1 pb-8 sm:pb-2 bg-gradient-to-b from-surface-900 to-surface-800">
	<div class="container mx-auto px-6">
		<div class="text-center mb-16">
			<div class="inline-flex items-center gap-4 mb-2 mr-8">
				<div class=" rounded-full flex items-center justify-center">
					<Camera size={24} class="text-white" />
				</div>
				<h2 class="text-4xl md:text-5xl font-bold text-white">Gallery</h2>
			</div>
		</div>

		<div
			class="transform transition-all duration-1000"
			class:translate-y-0={galleryVisible}
			class:translate-y-16={!galleryVisible}
			class:opacity-100={galleryVisible}
			class:opacity-0={!galleryVisible}
		>
			<div class="grid grid-cols-2 md:grid-cols-4 gap-6">
				{#each ['6nine_dj.JPG', 'floso-2024.JPG', 'P1010065.jpg', 'P1010180.jpg', 'partyBW.png', 'ybrshow1.jpg', 'ybrshow2.jpg', 'ybrshow3.jpg'] as filename, i}
					<div
						class="group aspect-square overflow-hidden rounded-2xl bg-surface-700 shadow-lg transform transition-all duration-500 hover:scale-105 hover:shadow-2xl"
						style="transition-delay: {i * 100}ms"
					>
						<img
							src={`/lib/assets/live/${filename}`}
							alt="Star6nine live performance"
							class="h-full w-full object-cover transition-all duration-500 group-hover:scale-110 group-hover:brightness-110"
						/>
					</div>
				{/each}
			</div>
		</div>
	</div>
</section>

<!-- BIOGRAPHY SECTION -->
<section
	class="pt-8 sm:pt-10 pb-8 sm:pb-2 bg-gradient-to-r from-primary-900/10 via-surface-800 to-secondary-900/10"
>
	<div class="container mx-auto px-6">
		<div class="max-w-4xl mx-auto">
			<div class="text-center mb-12">
				<div class="inline-flex items-center gap-3 mb-6">
					<div
						class="w-12 h-12 bg-gradient-to-r from-primary-500 to-secondary-500 rounded-full flex items-center justify-center"
					>
						<Users size={24} class="text-white" />
					</div>
					<h2 class="text-4xl md:text-5xl font-bold text-white">Biography</h2>
				</div>
			</div>

			<div class="space-y-8 text-lg leading-relaxed text-surface-200">
				<div class="grid md:grid-cols-2 gap-12 items-center">
					<div class="space-y-6">
						<p>
							Star6nine is a dubstep project started in 2021 by electronic music producer Adam
							Vacha. With a lifetime of music theory and composition training, *69 was started from
							scratch. The sounds herein hail from a foreign region of deep space that extends out
							into a signature dark bass music profile.
						</p>
						<p>
							From the age of 12 learning classical guitar and piano at the Center for the Arts
							program in St. Petersburg Florida, to the Pinellas County Center for the Arts Program
							for High School and eventually Berklee College of Music for music production, it is
							safe to say much training has been put into Star6nine's new iconic sound.
						</p>
					</div>
					<div class="space-y-6">
						<p>
							2 years were spent hidden away in recording studios to bring forth the best possible
							product and now is the time Star6nine hits the stage to show the world its new music.
						</p>
						<p>
							With 100's of hours performing on stage across the country, Star6nine is no stranger
							to live performance. Having run a recording studio on La Cienega Blvd in Hollywood CA
							while DJ'ing raves on the weekends in Los Angeles, not only has the time been put into
							the studio but the live sets as well. Unique and powerful double drops coupled with
							driving and extremely deep bass lead to live DJ sets that truly move the crowd.
						</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- NOTABLE PERFORMANCES -->
<section class="pt-8 sm:pt-10 pb-8 sm:pb-1 bg-surface-800 mt-2">
	<div class="container mx-auto px-6">
		<div class="text-center mb-16">
			<div class="inline-flex items-center gap-3 mb-6">
				<div
					class="w-12 h-12 bg-gradient-to-r from-secondary-500 to-primary-500 rounded-full flex items-center justify-center"
				>
					<Calendar size={24} class="text-white" />
				</div>
				<h2 class="text-4xl md:text-5xl font-bold text-white">Shows</h2>
			</div>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-6xl mx-auto">
			{#each [{ artist: 'Slightly Stoopid', venue: 'Official Reggae Rise Up After Party', location: 'St. Petersburg, FL' }, { artist: 'Eli Mac & Doom Flamingo', venue: 'Official Reggae Rise Up After Party', location: 'St. Petersburg, FL' }, { artist: 'G-Space & Milano', venue: 'Floridian Social', location: 'St. Petersburg, FL' }, { artist: 'Tie Dye Ky & Potions', venue: '1920', location: 'Ybor, FL' }, { artist: 'Torcha', venue: 'Mad Chiller', location: 'Tampa, FL' }, { artist: 'Headline Set', venue: 'Tk Lounge', location: 'Tampa, FL' }] as performance}
				<div
					class="group bg-gradient-to-br from-surface-700 to-surface-800 p-8 rounded-2xl shadow-lg hover:shadow-2xl transform hover:scale-105 transition-all duration-300 border border-surface-600/50"
				>
					<h3
						class="text-2xl font-bold text-primary-400 mb-3 group-hover:text-primary-300 transition-colors"
					>
						{performance.artist}
					</h3>
					<div class="space-y-2 text-surface-300">
						<p class="flex items-center gap-2">
							<Music size={16} />
							{performance.venue}
						</p>
						<p class="flex items-center gap-2">
							<MapPin size={16} />
							{performance.location}
						</p>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>

<!-- MUSIC SECTION -->
<section class="pt-8 sm:pt-20 pb-8 sm:pb-2 bg-gradient-to-b from-surface-800 to-surface-900">
	<div class="container mx-auto px-6">
		<div class="text-center mb-16">
			<div class="inline-flex items-center gap-3 mb-6">
				<div
					class="w-12 h-12 bg-gradient-to-r from-primary-500 to-secondary-500 rounded-full flex items-center justify-center"
				>
					<Music size={24} class="text-white" />
				</div>
				<h2 class="text-4xl md:text-5xl font-bold text-white">Music</h2>
			</div>
		</div>

		<div class="space-y-16 max-w-6xl mx-auto">
			<!-- Spotify Embed -->
			<div
				class="bg-surface-800/50 backdrop-blur-sm rounded-3xl p-8 shadow-2xl border border-surface-700/50"
			>
				<div class="flex items-center gap-3 mb-6">
					<IconBrandSpotify size={32} class="text-green-500" />
					<h3 class="text-2xl font-bold text-white">Latest Releases</h3>
				</div>
				<div class="rounded-2xl overflow-hidden shadow-lg">
					<iframe
						class="w-full"
						src="https://open.spotify.com/embed/artist/4PHiEApmqAZgGyCvaJopFb?utm_source=generator"
						title="Spotify"
						height="500"
						frameBorder="0"
						allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
						loading="lazy"
					>
					</iframe>
				</div>
			</div>

			<!-- SoundCloud Embed -->
			<div
				class="bg-surface-800/50 backdrop-blur-sm rounded-3xl p-8 shadow-2xl border border-surface-700/50"
			>
				<div class="flex items-center gap-3 mb-4">
					<IconCloud size={32} class="text-orange-500" />
					<h3 class="text-2xl font-bold text-white">Demo DJ Set</h3>
				</div>
				<div class="rounded-2xl overflow-hidden shadow-lg">
					<iframe
						title="soundcloud"
						width="100%"
						height="300"
						scrolling="no"
						frameborder="no"
						allow="autoplay"
						src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/2164381407%3Fsecret_token%3Ds-PjWHpNdu2S7&color=%23040404&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=false&visual=true"
					></iframe>
					<div
						style="font-size: 10px; color: #cccccc;line-break: anywhere;word-break: normal;overflow: hidden;white-space: nowrap;text-overflow: ellipsis; font-family: Interstate,Lucida Grande,Lucida Sans Unicode,Lucida Sans,Garuda,Verdana,Tahoma,sans-serif;font-weight: 100;"
					>
						<a
							href="https://soundcloud.com/starsixty_nine"
							title="Star6nine"
							target="_blank"
							style="color: #cccccc; text-decoration: none;">Star6nine</a
						>
						·
						<a
							href="https://soundcloud.com/starsixty_nine/demo-dj-set/s-PjWHpNdu2S7"
							title="Demo DJ Set"
							target="_blank"
							style="color: #cccccc; text-decoration: none;">Demo DJ Set</a
						>
					</div>
				</div>
				<div class="mt-4 text-center">
					<div class="inline-flex gap-4 text-sm text-surface-400">
						<a
							href="https://soundcloud.com/starsixty_nine"
							title="Star6nine"
							target="_blank"
							class="hover:text-primary-400 transition-colors"
						>
							Star6nine
						</a>
						<span>·</span>
						<a
							href="https://soundcloud.com/starsixty_nine/sets/demo"
							title="Demo"
							target="_blank"
							class="hover:text-primary-400 transition-colors"
						>
							Demo Collection
						</a>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- PRESS & FEATURES -->
<section class="pt-8 sm:pt-20 pb-8 sm:pb-2 bg-surface-800">
	<div class="container mx-auto px-6">
		<div class="text-center mb-16">
			<div class="inline-flex items-center gap-3 mb-6">
				<div
					class="w-12 h-12 bg-gradient-to-r from-secondary-500 to-primary-500 rounded-full flex items-center justify-center"
				>
					<FileText size={24} class="text-white" />
				</div>
				<h2 class="text-4xl md:text-5xl font-bold text-white">Press</h2>
			</div>
		</div>

		<div class="max-w-4xl mx-auto">
			<div
				class="bg-gradient-to-br from-surface-700 to-surface-800 rounded-3xl p-8 shadow-2xl border border-surface-600/50"
			>
				<div class="text-center">
					<img
						src="/lib/assets/press_1s69.png"
						alt="Star6nine Press Feature"
						class="w-full max-w-2xl mx-auto rounded-2xl shadow-lg"
					/>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- CONTACT CTA -->
<section class="py-8 sm:py-24 bg-gradient-to-r from-primary-900/20 via-surface-900 to-secondary-900/20">
	<div class="container mx-auto px-6 text-center">
		<p class="text-xl text-surface-300 mb-8 max-w-2xl mx-auto">
			For booking inquiries, press materials, or collaboration opportunities
		</p>
		<p class="text-xl text-surface-300 mb-8 max-w-2xl mx-auto">info@star6nice.space</p>
		<a
			href="mailto:info@star6nine.space"
			class="inline-flex items-center gap-3 bg-gradient-to-r from-primary-500 to-secondary-500 hover:from-primary-400 hover:to-secondary-400 px-8 py-4 rounded-full text-black font-semibold text-lg transition-all duration-300 transform hover:scale-105 shadow-lg hover:shadow-xl bg-white"
		>
			Get In Touch
		</a>
	</div>
</section>
