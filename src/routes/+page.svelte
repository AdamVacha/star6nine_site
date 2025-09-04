<script lang="ts">
	import SocialIcons from '$lib/components/SocialIcons.svelte';
</script>

<!-- LOGO -->
<section class="flex justify-center mx-6 mt-10">
	<div class="max-w-2xl">
		<img src="/lib/assets/star6ninelogo.png" alt="s69 logo" class="w-full" />
	</div>
</section>

<!-- SOCIAL ICONS -->
<section class="flex justify-center mt-0 mb-8">
	<SocialIcons />
</section>

<!-- SPOTIFY -->
<section class="flex justify-center items-center">
	<div class="w-full max-w-4xl px-4 md:mb-4 ">
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