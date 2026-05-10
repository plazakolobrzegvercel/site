<script lang="ts">
	import { fly } from 'svelte/transition';
	import { Umbrella, Car, Coffee, Waves } from '@lucide/svelte';
	import buildingImage from '$lib/assets/building.avif';
	import EnhancedImage from '$lib/components/EnhancedImage.svelte';

	const features = [
		{
			icon: Umbrella,
			title: '100m do plaży',
			description: 'Zaledwie 2 minuty spaceru od piaszczystej plaży w dzielnicy uzdrowiskowej'
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
		}
	];

	const stats = [
		{ value: '100m', label: 'do plaży' },
		{ value: '4', label: 'pokoje' },
		{ value: '8+', label: 'lat doświadczenia' },
		{ value: '100%', label: 'zadowolonych gości' }
	];

	let headerVisible = false;
	let photoVisible = false;
	let featuresVisible = false;
	let statsVisible = false;

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
		style="clip-path: ellipse(70% 100% at 50% 0%);"
	></div>

	<div class="relative z-10 container mx-auto max-w-350 px-6">
		<!-- Two-column layout -->
		<div class="mb-20 grid items-center gap-12 lg:grid-cols-2 lg:gap-16">
			<!-- Left column: text + features -->
			<div use:inview={() => (headerVisible = true)}>
				{#if headerVisible}
					<div transition:fly={{ x: -30, duration: 600 }}>
						<span
							class="mb-4 inline-block text-sm font-medium tracking-widest text-primary uppercase"
						>
							O nas
						</span>
						<h2 class="mb-6 font-display text-4xl font-semibold text-foreground md:text-5xl">
							Wypoczynek blisko morza
						</h2>
						<p class="mb-10 font-body text-lg leading-relaxed text-muted-foreground">
							Oferujemy apartamencik i 3 niezależne pokoje gościnne na ul. Kopernika w dzielnicy
							uzdrowiskowej Kołobrzegu, nieopodal najdłuższej w Polsce alei nadmorskiej – „Promenady
							Morskich Szeptów". Każdy pokój ma osobne wejście, więc możesz czuć się swobodnie i
							wracać kiedy zechcesz.
						</p>

						<!-- Features Grid -->
						<div use:inview={() => (featuresVisible = true)} class="grid gap-4 sm:grid-cols-2">
							{#each features as feature, index (index)}
								{#if featuresVisible}
									<div
										transition:fly={{ y: 20, duration: 500, delay: 200 + index * 100 }}
										class="group rounded-2xl bg-card p-5 shadow-soft transition-all duration-300 hover:-translate-y-1 hover:shadow-medium"
									>
										<div
											class="mb-3 flex h-10 w-10 items-center justify-center rounded-xl bg-linear-150 from-sea to-sea-light transition-transform duration-300 group-hover:scale-110"
										>
											<feature.icon class="h-5 w-5 text-primary-foreground" />
										</div>
										<h3 class="mb-1 font-display text-lg font-semibold text-foreground">
											{feature.title}
										</h3>
										<p class="font-body text-sm text-muted-foreground">
											{feature.description}
										</p>
									</div>
								{/if}
							{/each}
						</div>
					</div>
				{/if}
			</div>

			<!-- Right column: photo -->
			<div use:inview={() => (photoVisible = true)}>
				{#if photoVisible}
					<div
						transition:fly={{ x: 30, duration: 700, delay: 200 }}
						class="overflow-hidden rounded-2xl shadow-medium"
					>
						<EnhancedImage
							src={buildingImage}
							alt="Nasz obiekt - ul. Kopernika 7, Kołobrzeg"
							className="aspect-4/5 h-full w-full object-cover"
						/>
					</div>
				{/if}
			</div>
		</div>

		<!-- Stats -->
		<div use:inview={() => (statsVisible = true)} class="grid grid-cols-2 gap-8 md:grid-cols-4">
			{#each stats as stat, index (index)}
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
