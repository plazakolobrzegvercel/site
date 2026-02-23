<script>
	import heroImage from '$lib/assets/hero-beach.avif';
	import { MapPin } from '@lucide/svelte';

	import { fade, fly } from 'svelte/transition';
</script>

<section id="home" class="relative flex min-h-screen items-center justify-center overflow-hidden">
	<div class="absolute inset-0">
		<img src={heroImage} alt="Plaża w Kołobrzegu" class="h-full w-full object-cover" />
		<div
			class="absolute inset-0 bg-linear-to-b from-foreground/40 via-foreground/20 to-background/95"
		></div>
	</div>

	<div class="relative z-10 container mx-auto px-6 pt-24 pb-16 text-center">
		<div transition:fly={{ y: 40, duration: 800 }} class="mx-auto max-w-4xl">
			<div
				transition:fly={{ y: 40, duration: 800, delay: 200 }}
				class="mb-8 inline-flex items-center gap-2 rounded-full bg-white/90 px-4 py-2 text-sm font-medium text-foreground shadow-soft backdrop-blur-sm"
			>
				<MapPin class="h-4 w-4 text-primary" />
				<span>ul. Kopernika 7/1, Kołobrzeg</span>
			</div>

			<h1
				transition:fly={{ y: 30, duration: 800, delay: 200 }}
				class="mb-6 font-display text-5xl leading-22 font-bold text-white drop-shadow-lg md:text-7xl lg:text-8xl"
			>
				Twój{' '}
				<span class="text-cream">wymarzony</span>
				<br />
				wypoczynek
			</h1>

			<p
				transition:fly={{ y: 20, duration: 800, delay: 500 }}
				class="mx-auto mb-10 max-w-2xl font-body text-lg leading-relaxed text-white/90 drop-shadow-md md:text-xl"
			>
				Komfortowe pokoje gościnne zaledwie 150 metrów od plaży. Idealne miejsce na wakacyjny relaks
				nad Morzem Bałtyckim.
			</p>

			<div
				transition:fly={{ y: 20, duration: 800, delay: 700 }}
				class="flex flex-col items-center justify-center gap-4 sm:flex-row"
			>
				<a
					href="#rooms"
					class="group rounded-full bg-linear-to-r from-sea to-sea-light px-8 py-4 font-medium text-primary-foreground shadow-medium transition-all duration-300 hover:scale-105 hover:shadow-glow"
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

	<div
		transition:fade={{ duration: 800, delay: 1200 }}
		class="absolute bottom-6 left-1/2 -translate-x-1/2 animate-bounce"
	>
		<div
			class="flex h-10 w-6 items-start justify-center rounded-full border-2 border-foreground/30 p-2"
		>
			<div class="h-3 w-1.5 rounded-full bg-primary"></div>
		</div>
	</div>
</section>
