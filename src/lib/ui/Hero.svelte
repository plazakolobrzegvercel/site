<script lang="ts">
	import heroImage from '$lib/assets/hero-beach.avif';
	import { MapPin } from '@lucide/svelte';

	let sectionEl: HTMLElement;
	let visible = $state(false);

	$effect(() => {
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) {
					visible = true;
					observer.disconnect();
				}
			},
			{ threshold: 0.1 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	bind:this={sectionEl}
	id="home"
	class="relative flex min-h-screen items-center justify-center overflow-hidden"
>
	<div class="absolute inset-0">
		<img src={heroImage} alt="Plaża w Kołobrzegu" class="h-full w-full object-cover" />
		<div
			class="absolute inset-0 bg-linear-to-b from-foreground/40 via-foreground/20 to-background/95"
		></div>
	</div>

	<div class="relative z-10 container mx-auto px-6 pt-24 pb-16 text-center">
		<div class="mx-auto max-w-4xl">
			<div
				class="mb-8 inline-flex items-center gap-2 rounded-full bg-white/90 px-4 py-2 text-sm font-medium text-foreground shadow-soft backdrop-blur-sm transition-all duration-500 {visible
					? 'translate-y-0 opacity-100'
					: 'translate-y-10 opacity-0'}"
			>
				<MapPin class="h-4 w-4 text-primary" />
				<span>ul. Kopernika 7/1, Kołobrzeg</span>
			</div>

			<h1
				class="mb-6 font-display text-5xl leading-22 font-bold text-white drop-shadow-lg transition-all delay-100 duration-500 md:text-7xl lg:text-8xl {visible
					? 'translate-y-0 opacity-100'
					: 'translate-y-8 opacity-0'}"
			>
				Twój{' '}
				<span class="text-cream">wymarzony</span>
				<br />
				wypoczynek
			</h1>

			<p
				class="mx-auto mb-10 max-w-2xl font-body text-lg leading-relaxed text-white/90 drop-shadow-md transition-all delay-200 duration-500 md:text-xl {visible
					? 'translate-y-0 opacity-100'
					: 'translate-y-5 opacity-0'}"
			>
				Komfortowe pokoje gościnne zaledwie 150 metrów od plaży. Idealne miejsce na wakacyjny relaks
				nad Morzem Bałtyckim.
			</p>

			<div
				class="flex flex-col items-center justify-center gap-4 transition-all delay-300 duration-500 sm:flex-row {visible
					? 'translate-y-0 opacity-100'
					: 'translate-y-5 opacity-0'}"
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
		class="absolute bottom-6 left-1/2 -translate-x-1/2 animate-bounce transition-opacity delay-500 duration-500 {visible
			? 'opacity-100'
			: 'opacity-0'}"
	>
		<div
			class="flex h-10 w-6 items-start justify-center rounded-full border-2 border-foreground/30 p-2"
		>
			<div class="h-3 w-1.5 rounded-full bg-primary"></div>
		</div>
	</div>
</section>
