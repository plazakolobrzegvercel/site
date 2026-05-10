<script lang="ts">
	import { fly } from 'svelte/transition';
	import { Home, Heart, Users, HandCoins, TreePine, Sparkles } from '@lucide/svelte';
	import gardenImage from '$lib/assets/garden.avif';
	import EnhancedImage from '$lib/components/EnhancedImage.svelte';

	let photoVisible = false;
	let contentVisible = false;
	let highlightsVisible = false;

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

	const highlights = [
		{
			icon: Home,
			title: 'Spokój i cisza',
			description:
				'Zaciszna lokalizacja w dzielnicy uzdrowiskowej, z dala od zgiełku - idealna na regenerację sił.'
		},
		{
			icon: Heart,
			title: 'Domowy klimat',
			description:
				'Prowadzimy nasz domek osobiście, z sercem i dbałością o każdy detal. To nie hotel - to dom, w którym jesteś gościem.'
		},
		{
			icon: Users,
			title: 'Osobiste podejście',
			description:
				'Właściciele doglądają obiektu na co dzień. Każdy gość jest dla nas ważny i traktowany indywidualnie.'
		},
		{
			icon: HandCoins,
			title: 'Elastyczne ceny',
			description:
				'Ceny ustalamy indywidualnie - zależnie od liczby osób, terminu i długości pobytu. Zawsze warto zapytać!'
		},
		{
			icon: TreePine,
			title: 'Ogród do odpoczynku',
			description:
				'Do dyspozycji zaciszny zakątek w ogrodzie - odpoczywaj pośród kwiatów i napij się ulubionego napoju.'
		},
		{
			icon: Sparkles,
			title: 'Czystość i higiena',
			description:
				'Apartamencik i pokoje sprzątamy osobiście, dokładnie i regularnie. Przed przyjazdem gości ozonujemy pomieszczenia.'
		}
	];
</script>

<section class="bg-gradient-sea relative overflow-hidden py-24" id="atmosphere">
	<div
		class="absolute top-10 right-10 h-72 w-72 rounded-full bg-primary-foreground/5 blur-3xl"
	></div>
	<div
		class="absolute bottom-10 left-10 h-56 w-56 rounded-full bg-primary-foreground/5 blur-3xl"
	></div>

	<div class="relative z-10 container mx-auto px-6">
		<div class="grid items-center gap-12 lg:grid-cols-2 lg:gap-16">
			<!-- Left column: photo -->
			<div use:inview={() => (photoVisible = true)} class="order-2 lg:order-1">
				{#if photoVisible}
					<div
						transition:fly={{ x: -30, duration: 700 }}
						class="overflow-hidden rounded-2xl shadow-medium"
					>
						<EnhancedImage
							src={gardenImage}
							alt="Ogród z miejscem do wypoczynku – ławki i stół wśród zieleni"
							className="aspect-4/5 h-full w-full object-cover"
						/>
					</div>
				{/if}
			</div>

			<!-- Right column: text + highlights -->
			<div use:inview={() => (contentVisible = true)} class="order-1 lg:order-2">
				{#if contentVisible}
					<div transition:fly={{ x: 30, duration: 600 }}>
						<span
							class="mb-4 inline-block text-sm font-medium tracking-widest text-primary-foreground/70 uppercase"
						>
							Nasz klimat
						</span>
						<h2
							class="mb-6 font-display text-4xl font-semibold text-primary-foreground md:text-5xl"
						>
							Poczuj się jak u siebie
						</h2>
						<p class="mb-10 font-body text-lg leading-relaxed text-primary-foreground/80">
							Nasz domek na ul. Kopernika w Kołobrzegu to miejsce prowadzone z pasją i sercem. Nie
							jesteśmy hotelem - jesteśmy rodziną, która chce, żebyś wypoczął jak najlepiej. Spokój,
							prywatność i domowa atmosfera - to nasze priorytety.
						</p>

						<div use:inview={() => (highlightsVisible = true)} class="grid gap-4 sm:grid-cols-2">
							{#each highlights as item, index (index)}
								{#if highlightsVisible}
									<div
										transition:fly={{ y: 20, duration: 500, delay: 200 + index * 100 }}
										class="group rounded-2xl border border-primary-foreground/10 bg-primary-foreground/10 p-4 backdrop-blur-sm transition-all duration-300 hover:bg-primary-foreground/15"
									>
										<div
											class="mb-3 flex h-10 w-10 items-center justify-center rounded-xl bg-primary-foreground/15 transition-transform duration-300 group-hover:scale-110"
										>
											<item.icon class="h-5 w-5 text-primary-foreground" />
										</div>
										<h3 class="mb-1 font-display text-lg font-semibold text-primary-foreground">
											{item.title}
										</h3>
										<p class="font-body text-sm leading-relaxed text-primary-foreground/70">
											{item.description}
										</p>
									</div>
								{/if}
							{/each}
						</div>
					</div>
				{/if}
			</div>
		</div>
	</div>
</section>
