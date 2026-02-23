<script lang="ts">
	import { fly } from 'svelte/transition';
	import { Umbrella, Wifi, Car, Coffee, Waves, Heart } from '@lucide/svelte';

	const features = [
		{
			icon: Umbrella,
			title: '150m do plaży',
			description: 'Zaledwie 2 minuty spaceru od piaszczystej plaży'
		},
		{
			icon: Wifi,
			title: 'Darmowe WiFi',
			description: 'Szybki internet w każdym pokoju'
		},
		{
			icon: Car,
			title: 'Bezpłatny parking',
			description: 'Wygodne miejsce parkingowe przy obiekcie'
		},
		{
			icon: Coffee,
			title: 'Aneks kuchenny',
			description: 'Pełne wyposażenie kuchenne do samodzielnej kuchni'
		},
		{
			icon: Waves,
			title: 'Sprzęt plażowy',
			description: 'Leżaki, parawan i ręczniki w zestawie'
		},
		{
			icon: Heart,
			title: 'Domowa atmosfera',
			description: 'Przytulne pokoje z indywidualnym podejściem'
		}
	];

	const stats = [
		{ value: '150m', label: 'do plaży' },
		{ value: '4', label: 'pokoje' },
		{ value: '8+', label: 'lat doświadczenia' },
		{ value: '100%', label: 'zadowolonych gości' }
	];

	let headerVisible = $state(false);
	let featuresVisible = $state(false);
	let statsVisible = $state(false);

	function inview(node: HTMLElement, onVisible: () => void) {
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						onVisible();
						observer.unobserve(node);
					}
				}
			},
			{ threshold: 0.2 }
		);
		observer.observe(node);
		return {
			destroy() {
				observer.disconnect();
			}
		};
	}
</script>

<section id="about" class="relative overflow-hidden bg-linear-180 from-sand to-cream py-24">
	<div
		class="absolute top-0 right-0 left-0 h-24 bg-background"
		style="
			clipPath: ellipse(70% 100% at 50% 0%);
		"
	></div>

	<div class="relative z-10 container mx-auto max-w-350 px-6">
		<div use:inview={() => (headerVisible = true)} class="mx-auto mb-16 max-w-3xl text-center">
			{#if headerVisible}
				<div transition:fly={{ y: 30, duration: 600 }}>
					<span
						class="mb-4 inline-block text-sm font-medium tracking-widest text-primary uppercase"
					>
						O nas
					</span>
					<h2 class="mb-6 font-display text-4xl font-semibold text-foreground md:text-5xl">
						Wypoczynek blisko morza
					</h2>
					<p class="font-body text-lg leading-relaxed text-muted-foreground">
						Oferujemy komfortowe pokoje gościnne w samym sercu Kołobrzegu. Nasz obiekt to idealne
						miejsce dla osób szukających spokoju, bliskości morza i domowej atmosfery. Zapraszamy do
						nas rodziny, pary oraz podróżników ceniących przytulne, dobrze wyposażone wnętrza.
					</p>
				</div>
			{/if}
		</div>

		<div
			use:inview={() => (featuresVisible = true)}
			class="grid gap-6 md:grid-cols-2 lg:grid-cols-3"
		>
			{#each features as feature, index}
				{#if featuresVisible}
					<div
						transition:fly={{ y: 30, duration: 500, delay: index * 150 }}
						class="group rounded-2xl bg-card p-6 shadow-soft transition-all duration-300 hover:-translate-y-1 hover:shadow-medium"
					>
						<div
							class="mb-4 flex h-12 w-12 items-center justify-center rounded-xl bg-linear-150 from-sea to-sea-light transition-transform duration-300 group-hover:scale-110"
						>
							<feature.icon class="h-6 w-6 text-primary-foreground" />
						</div>
						<h3 class="mb-2 font-display text-xl font-bold text-foreground">
							{feature.title}
						</h3>
						<p class="font-body text-muted-foreground">
							{feature.description}
						</p>
					</div>
				{/if}
			{/each}
		</div>

		<div
			use:inview={() => (statsVisible = true)}
			class="mt-20 grid grid-cols-2 gap-8 md:grid-cols-4"
		>
			{#each stats as stat, index}
				{#if statsVisible}
					<div
						transition:fly={{ y: 30, duration: 600, delay: 600 + index * 100 }}
						class="text-center"
					>
						<div class="mb-2 font-display text-4xl font-bold text-primary md:text-5xl">
							{stat.value}
						</div>
						<div class="font-body text-sm tracking-wide text-muted-foreground uppercase">
							{stat.label}
						</div>
					</div>
				{/if}
			{/each}
		</div>
	</div>
</section>
