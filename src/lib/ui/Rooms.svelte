<script lang="ts">
	import { fly } from 'svelte/transition';
	import { Users, Maximize, ChefHat, Bath, ChevronLeft, ChevronRight, X } from '@lucide/svelte';

	import apartamencik1 from '$lib/assets/rooms/apartamencik-1.avif';
	import apartamencik2 from '$lib/assets/rooms/apartamencik-2.avif';
	import apartamencikExterior from '$lib/assets/rooms/apartamencik-exterior.avif';
	import pokoj1_1 from '$lib/assets/rooms/pokoj1-1.avif';
	import pokoj1_2 from '$lib/assets/rooms/pokoj1-2.avif';
	import pokoj2_1 from '$lib/assets/rooms/pokoj2-1.avif';

	const rooms = [
		{
			id: 1,
			name: 'Apartamencik',
			subtitle: 'Niezależne mieszkanie dla 2 osób',
			description:
				'Nowoczesne, w pełni wyposażone mieszkanie-kawalerka z aneksem kuchennym i łazienką. Do dyspozycji: kuchnia gazowa, zmywarka, lodówka z zamrażalnikiem, telewizor, a w łazience prysznic i pralka.',
			images: [apartamencik1, apartamencik2, apartamencikExterior],
			features: [
				{ icon: Users, text: '2 osoby' },
				{ icon: ChefHat, text: 'Aneks kuchenny' },
				{ icon: Bath, text: 'Prywatna łazienka' }
			]
		},
		{
			id: 2,
			name: 'Pokój nr 1',
			subtitle: 'Przytulny pokój dla 2 osób',
			description:
				'Kameralny pokój dla dwóch osób z łazienką i aneksem kuchennym – idealny na wakacyjny pobyt nad morzem. W aneksie lodówka, kuchenka elektryczna, czajnik oraz komplet naczyń.',
			images: [pokoj1_1, pokoj1_2],
			features: [
				{ icon: Users, text: '2 osoby' },
				{ icon: ChefHat, text: 'Aneks kuchenny' },
				{ icon: Bath, text: 'Prywatna łazienka' }
			]
		},
		{
			id: 3,
			name: 'Pokój nr 2',
			subtitle: 'Komfortowy pokój dla 2 osób',
			description:
				'Wygodny pokój dwuosobowy z własną łazienką i aneksem kuchennym. Idealny dla par lub przyjaciół szukających spokojnego miejsca blisko morza.',
			images: [pokoj2_1],
			features: [
				{ icon: Users, text: '2 osoby' },
				{ icon: ChefHat, text: 'Aneks kuchenny' },
				{ icon: Bath, text: 'Prywatna łazienka' }
			]
		},
		{
			id: 4,
			name: 'Pokój nr 3',
			subtitle: 'Pokój dla 2 osób',
			description:
				'Przytulny pokój dwuosobowy z dostępem do łazienki. Wyposażony w wygodne łóżka, telewizor oraz podstawowe udogodnienia na czas pobytu.',
			images: [pokoj1_1],
			features: [
				{ icon: Users, text: '2 osoby' },
				{ icon: Maximize, text: 'Przestronny' },
				{ icon: Bath, text: 'Łazienka' }
			]
		}
	];

	let headerVisible = $state(false);
	let cardsVisible = $state(false);

	let galleryOpen = $state(false);
	let galleryImages = $state<string[]>([]);
	let galleryIndex = $state(0);

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

	function openGallery(images: string[]) {
		galleryImages = images;
		galleryIndex = 0;
		galleryOpen = true;
	}

	function closeGallery() {
		galleryOpen = false;
	}

	function prevImage() {
		galleryIndex = (galleryIndex - 1 + galleryImages.length) % galleryImages.length;
	}

	function nextImage() {
		galleryIndex = (galleryIndex + 1) % galleryImages.length;
	}

	function handleKeydown(e: KeyboardEvent) {
		if (!galleryOpen) return;
		if (e.key === 'Escape') closeGallery();
		if (e.key === 'ArrowLeft') prevImage();
		if (e.key === 'ArrowRight') nextImage();
	}
</script>

<svelte:window onkeydown={handleKeydown} />

<section id="rooms" class="relative bg-card py-24">
	<div class="container mx-auto max-w-350 px-6">
		<div use:inview={() => (headerVisible = true)} class="mx-auto mb-16 max-w-2xl text-center">
			{#if headerVisible}
				<div transition:fly={{ y: 30, duration: 600 }}>
					<span
						class="mb-4 inline-block text-sm font-medium tracking-widest text-primary uppercase"
					>
						Nasze pokoje
					</span>
					<h2 class="mb-6 font-display text-4xl font-semibold text-foreground md:text-5xl">
						Wybierz idealny pokój
					</h2>
					<p class="font-body text-lg leading-relaxed text-muted-foreground">
						Każdy z naszych pokojów jest przytulnie urządzony i wyposażony we wszystko, czego
						potrzebujesz na wakacyjny wypoczynek.
					</p>
				</div>
			{/if}
		</div>

		<div use:inview={() => (cardsVisible = true)} class="grid gap-8 md:grid-cols-2">
			{#each rooms as room, index (room.id)}
				{#if cardsVisible}
					<article
						transition:fly={{ y: 30, duration: 500, delay: index * 150 }}
						class="group overflow-hidden rounded-2xl bg-background shadow-soft transition-all duration-500 hover:shadow-medium"
					>
						<button
							type="button"
							class="relative aspect-4/3 w-full cursor-pointer overflow-hidden"
							onclick={() => openGallery(room.images)}
						>
							<img
								src={room.images[0]}
								alt={room.name}
								class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
							/>
							<div
								class="absolute inset-0 bg-linear-to-t from-foreground/60 via-transparent to-transparent opacity-0 transition-opacity duration-300 group-hover:opacity-100"
							></div>

							<div
								class="absolute inset-0 flex items-center justify-center opacity-0 transition-opacity duration-300 group-hover:opacity-100"
							>
								<span
									class="rounded-full bg-card/90 px-6 py-3 text-sm font-medium text-foreground backdrop-blur-sm"
								>
									Zobacz galerię ({room.images.length} zdjęć)
								</span>
							</div>
						</button>

						<div class="p-6">
							<h3 class="mb-1 font-display text-2xl font-semibold text-foreground">
								{room.name}
							</h3>
							<p class="mb-4 font-body font-medium text-primary">
								{room.subtitle}
							</p>
							<p class="mb-6 line-clamp-3 font-body text-sm text-muted-foreground">
								{room.description}
							</p>

							<div class="mb-6 flex flex-wrap gap-3">
								{#each room.features as feature, idx (idx)}
									<div class="flex items-center gap-2 rounded-full bg-muted px-3 py-1.5 text-sm">
										<feature.icon class="h-4 w-4 text-primary" />
										<span class="text-foreground/80">{feature.text}</span>
									</div>
								{/each}
							</div>

							<a
								href="#contact"
								class="bg-gradient-sea inline-flex items-center gap-2 rounded-full px-6 py-3 font-medium text-primary-foreground transition-all duration-300 hover:scale-105 hover:shadow-glow"
							>
								Zarezerwuj
							</a>
						</div>
					</article>
				{/if}
			{/each}
		</div>
	</div>

	{#if galleryOpen}
		<div
			class="fixed inset-0 z-50 flex items-center justify-center bg-foreground/80 backdrop-blur-sm"
			role="dialog"
			aria-modal="true"
		>
			<button
				type="button"
				class="absolute inset-0 cursor-default"
				onclick={closeGallery}
				aria-label="Zamknij galerię"
			></button>

			<button
				type="button"
				onclick={closeGallery}
				class="absolute top-4 right-4 z-10 flex h-10 w-10 cursor-pointer items-center justify-center rounded-full bg-card/90 text-foreground backdrop-blur-sm transition-colors hover:bg-card"
				aria-label="Zamknij"
			>
				<X class="h-5 w-5" />
			</button>

			{#if galleryImages.length > 1}
				<button
					type="button"
					onclick={prevImage}
					class="absolute left-4 z-10 flex h-10 w-10 cursor-pointer items-center justify-center rounded-full bg-card/90 text-foreground backdrop-blur-sm transition-colors hover:bg-card"
					aria-label="Poprzednie zdjęcie"
				>
					<ChevronLeft class="h-5 w-5" />
				</button>

				<button
					type="button"
					onclick={nextImage}
					class="absolute right-4 z-10 flex h-10 w-10 cursor-pointer items-center justify-center rounded-full bg-card/90 text-foreground backdrop-blur-sm transition-colors hover:bg-card"
					aria-label="Następne zdjęcie"
				>
					<ChevronRight class="h-5 w-5" />
				</button>
			{/if}

			<div class="relative z-10 max-h-[85vh] max-w-[90vw]">
				{#key galleryIndex}
					<img
						src={galleryImages[galleryIndex]}
						alt="Zdjęcie {galleryIndex + 1} z {galleryImages.length}"
						class="max-h-[85vh] max-w-[90vw] rounded-lg object-contain shadow-lg"
					/>
				{/key}
			</div>

			{#if galleryImages.length > 1}
				<div
					class="absolute bottom-4 left-1/2 z-10 -translate-x-1/2 rounded-full bg-card/90 px-4 py-2 text-sm font-medium text-foreground backdrop-blur-sm"
				>
					{galleryIndex + 1} / {galleryImages.length}
				</div>
			{/if}
		</div>
	{/if}
</section>
