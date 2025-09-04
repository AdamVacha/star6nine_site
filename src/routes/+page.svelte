<script lang="ts">
	import SocialIcons from '$lib/components/SocialIcons.svelte';
</script>

<!-- SOCIAL ICONS -->
<section class="flex justify-center mt-12 mb-10 lg:mb-0">
	<SocialIcons />
</section>

<!-- LOGO -->
<section class="flex justify-center m-6 mb-10 sm:mb-0 -mt-5 sm:-mt-0">
	<div class="max-w-2xl">
		<img src="/lib/assets/star6ninelogo.png" alt="s69 logo" class="w-full" />
	</div>
</section>

<!-- SPOTIFY -->
<section class="flex justify-center items-center mb-4">
	<div class="w-full max-w-4xl px-4">
		<iframe
			class="w-full rounded-2xl"
			src="https://open.spotify.com/embed/artist/4PHiEApmqAZgGyCvaJopFb?utm_source=generator"
			title="Spotify"
			height="400"
			frameBorder="0"
			allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
			loading="lazy"
		>
		</iframe>
	</div>
</section>
