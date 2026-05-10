<script>
	import { fade } from 'svelte/transition';
	import heroImage from '$lib/assets/hero-beach.avif';
	import logo from '$lib/assets/logo.avif';

	let scrollY = 0;
</script>

<svelte:window bind:scrollY />

<section
	id="home"
	class="relative flex min-h-[70vh] items-center justify-center overflow-hidden md:min-h-[75vh]"
>
	<div class="absolute inset-0">
		<img
			src={heroImage}
			alt="Plaża w Kołobrzegu"
			class="h-full w-full object-cover"
			loading="eager"
		/>
		<div
			class="absolute inset-0 bg-gradient-to-b from-foreground/40 via-foreground/20 to-background/95"
		></div>
	</div>

	<div class="relative z-10 container mx-auto px-6 py-16 pt-24 text-center">
		<div class="mx-auto max-w-4xl" transition:fade={{ duration: 800 }}>
			<img
				src={logo}
				alt="Plaza Blisko - Pokoje Gościnne Kołobrzeg"
				class="mx-auto mb-10 w-full max-w-2xl drop-shadow-2xl md:max-w-3xl lg:max-w-4xl"
				width="600"
				height="200"
				loading="eager"
			/>

			<div
				class="flex flex-col items-center justify-center gap-4 sm:flex-row"
				transition:fade={{ duration: 600, delay: 700 }}
			>
				<a
					href="#rooms"
					class="group bg-gradient-sea rounded-full px-8 py-4 font-medium text-primary-foreground shadow-medium transition-all duration-300 hover:scale-105 hover:shadow-glow"
				>
					<span>Zobacz pokoje</span>
				</a>
				<a
					href="#contact"
					class="rounded-full bg-card/80 px-8 py-4 font-medium text-foreground shadow-soft backdrop-blur-sm transition-all duration-300 hover:scale-105 hover:shadow-medium"
				>
					Kontakt
				</a>
			</div>
		</div>
	</div>

	<div class="absolute bottom-6 left-1/2 -translate-x-1/2" transition:fade={{ delay: 1200 }}>
		<div
			class="flex items-start justify-center rounded-full border-2 border-foreground/30 p-2"
			style="width: 1.5rem; height: 2.5rem; animation: scroll-bounce 1.5s infinite;"
		>
			<div class="h-3 w-1.5 rounded-full bg-primary"></div>
		</div>
	</div>
</section>

<style>
	@keyframes scroll-bounce {
		0%,
		100% {
			transform: translateY(0);
		}
		50% {
			transform: translateY(10px);
		}
	}
</style>
