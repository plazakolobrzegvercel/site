<script lang="ts">
	import { fly, fade, scale } from 'svelte/transition';
	import {
		Users,
		ChefHat,
		Bath,
		ChevronLeft,
		ChevronRight,
		X,
		Tv,
		Refrigerator,
		Eye,
		Info
	} from '@lucide/svelte';

	import apartamencik1 from '$lib/assets/rooms/apartamencik-1.avif';
	import apartamencik2 from '$lib/assets/rooms/apartamencik-2.avif';
	import apartamencikExterior from '$lib/assets/rooms/apartamencik-exterior.avif';
	import pokoj1_1 from '$lib/assets/rooms/pokoj1-1.avif';
	import pokoj1_2 from '$lib/assets/rooms/pokoj1-2.avif';
	import pokoj2_1 from '$lib/assets/rooms/pokoj2-1.avif';

	import type { Component } from 'svelte';

	interface Room {
		id: number;
		name: string;
		subtitle: string;
		shortDescription: string;
		fullDescription: string;
		thumbnail: string;
		images: string[];
		equipment: string[];
		keyFeatures: { icon: Component<{ class?: string }>; text: string }[];
	}

	const rooms: Room[] = [
		{
			id: 1,
			name: 'Apartamencik',
			subtitle: 'Niezależne mieszkanie dla 2 osób',
			shortDescription:
				'Nowoczesne, w pełni wyposażone mieszkanie-kawalerka z aneksem kuchennym i łazienką. Osobne wejście i ganek.',
			fullDescription:
				'Nowoczesne, w pełni wyposażone mieszkanie-kawalerka dla 2 osób z aneksem kuchennym i łazienką. Do dyspozycji: kuchnia gazowa, zmywarka, lodówka z zamrażalnikiem, telewizor, a w łazience prysznic i pralka. Wygodne łóżka 80×200 cm można zestawić lub rozsunąć. Przemyślany układ zapewnia komfort i funkcjonalność. Ciepłą wodę i ogrzewanie zapewnia dwufunkcyjny piecyk gazowy. Na wyposażeniu ręczniki, parawan i leżaki plażowe – idealne na relaks nad morzem!',
			thumbnail: apartamencik1,
			images: [
				apartamencik1,
				apartamencik2,
				apartamencikExterior,
				'https://plazablisko.pl/wp-content/uploads/2025/01/IMG_2037-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2025/01/IMG_2035-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2025/01/IMG_2034-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2025/01/IMG_2032-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.33.52-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2020/07/Apartament-7-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.34.13-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2020/08/image2-scaled.jpeg'
			],
			equipment: [
				'Kuchnia gazowa',
				'Zmywarka',
				'Lodówka z zamrażalnikiem',
				'Telewizor',
				'Prysznic',
				'Pralka',
				'Łóżka 80×200 cm',
				'Ręczniki',
				'Parawan plażowy',
				'Leżaki plażowe',
				'Osobne wejście'
			],
			keyFeatures: [
				{ icon: Users, text: '2 osoby' },
				{ icon: ChefHat, text: 'Kuchnia gazowa' },
				{ icon: Bath, text: 'Prywatna łazienka' },
				{ icon: Refrigerator, text: 'Pralka' }
			]
		},
		{
			id: 2,
			name: 'Pokój nr 1',
			subtitle: 'Przytulny pokój dla 2 osób blisko plaży',
			shortDescription:
				'Kameralny pokój z łazienką i aneksem kuchennym – idealny na wakacyjny pobyt nad morzem.',
			fullDescription:
				'Kameralny pokój dla dwóch osób z łazienką i aneksem kuchennym – idealny na wakacyjny pobyt nad morzem. W aneksie kuchennym znajduje się lodówka z zamrażalnikiem, kuchenka elektryczna, czajnik oraz komplet naczyń i sztućców. W łazience dostępne są prysznic, umywalka i toaleta, a w pokoju pojemna szafa, telewizor oraz wszystko, co potrzebne do wypoczynku. Na wyposażeniu czekają również ręczniki, parawan i leżaki plażowe – idealne na leniwe dni na plaży.',
			thumbnail: pokoj1_1,
			images: [
				pokoj1_1,
				pokoj1_2,
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.48.47-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.49.12-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.39.30-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2021/07/1625930745702-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.48.56-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.41.22-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.49.40-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.49.25-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/01/pokoj-1-lazienka-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30-08.41.40-scaled.jpg'
			],
			equipment: [
				'Lodówka z zamrażalnikiem',
				'Kuchenka elektryczna',
				'Czajnik',
				'Komplet naczyń i sztućców',
				'Telewizor',
				'Szafa',
				'Prysznic',
				'Ręczniki',
				'Parawan plażowy',
				'Leżaki plażowe'
			],
			keyFeatures: [
				{ icon: Users, text: '2 osoby' },
				{ icon: ChefHat, text: 'Aneks kuchenny' },
				{ icon: Bath, text: 'Prywatna łazienka' },
				{ icon: Tv, text: 'Telewizor' }
			]
		},
		{
			id: 3,
			name: 'Pokój nr 2',
			subtitle: 'Pokój dla 2 osób z widokiem na ulicę',
			shortDescription:
				'Pokój z łazienką i aneksem kuchennym. Wygodne hotelowe łóżka można zestawić lub rozsunąć.',
			fullDescription:
				'Pokój dla 2 osób z łazienką i aneksem kuchennym, wyposażony w lodówkę z zamrażalnikiem, kuchenkę elektryczną, czajnik i telewizor. W kuchni znajdują się wszystkie niezbędne akcesoria – talerzyki, kubki, sztućce, garnek, patelnia i inne. Ręczniki są na wyposażeniu. Wygodne hotelowe łóżka można zestawić lub rozsunąć według potrzeb. Z okna roztacza się widok na parking i ulicę Kopernika.',
			thumbnail: pokoj2_1,
			images: [
				pokoj2_1,
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.42.08-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.45.16-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.43.46-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.43.58-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.44.02-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.44.20-1-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.42.33-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.42.50-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/06/2024-05-30_08.42.57-scaled.jpg'
			],
			equipment: [
				'Lodówka z zamrażalnikiem',
				'Kuchenka elektryczna',
				'Czajnik',
				'Komplet naczyń i sztućców',
				'Garnek, patelnia',
				'Telewizor',
				'Ręczniki',
				'Łóżka hotelowe (można rozstawić)'
			],
			keyFeatures: [
				{ icon: Users, text: '2 osoby' },
				{ icon: ChefHat, text: 'Aneks kuchenny' },
				{ icon: Bath, text: 'Prywatna łazienka' },
				{ icon: Eye, text: 'Widok na ulicę' }
			]
		},
		{
			id: 4,
			name: 'Pokój nr 3',
			subtitle: 'Przytulny pokój dla 2 osób',
			shortDescription:
				'Pokój z lodówką, czajnikiem, telewizorem i prywatną łazienką z wanną na korytarzu.',
			fullDescription:
				'Przytulny pokój dla 2 osób, idealny na spokojny wypoczynek nad morzem. Wygodne hotelowe łóżka, telewizor, lodówka z zamrażalnikiem, czajnik oraz komplet naczyń i sztućców zapewniają komfort pobytu. Do dyspozycji gości szafa, stół i krzesła, a także prywatna łazienka na korytarzu wyposażona w wannę z prysznicem, toaletę i umywalkę. W cenie ręczniki, parawan i leżaki plażowe.',
			thumbnail: 'https://plazablisko.pl/wp-content/uploads/2024/05/2024-05-26-21.01.01-scaled.jpg',
			images: [
				'https://plazablisko.pl/wp-content/uploads/2024/05/2024-05-26-21.01.01-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/05/2024-05-26-21.00.13-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/05/2024-05-26-21.00.57-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/05/2024-05-26-20.59.45-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2024/05/2024-05-26-20.58.57-scaled.jpg',
				'https://plazablisko.pl/wp-content/uploads/2020/07/lazienka-1.jpg'
			],
			equipment: [
				'Lodówka z zamrażalnikiem',
				'Czajnik',
				'Komplet naczyń i sztućców',
				'Telewizor',
				'Szafa',
				'Stół i krzesła',
				'Wanna z prysznicem',
				'Ręczniki',
				'Parawan plażowy',
				'Leżaki plażowe'
			],
			keyFeatures: [
				{ icon: Users, text: '2 osoby' },
				{ icon: Refrigerator, text: 'Lodówka' },
				{ icon: Bath, text: 'Łazienka z wanną' },
				{ icon: Tv, text: 'Telewizor' }
			]
		}
	];

	import EnhancedImage from '$lib/components/EnhancedImage.svelte';

	let headerVisible = false;
	let cardsVisible = false;

	let galleryRoom: Room | null = null;
	let galleryIndex = 0;

	let detailRoom: Room | null = null;

	function openGallery(room: Room) {
		galleryIndex = 0;
		galleryRoom = room;
	}
	function closeGallery() {
		galleryRoom = null;
	}
	function prevImage() {
		if (!galleryRoom) return;
		galleryIndex = (galleryIndex - 1 + galleryRoom.images.length) % galleryRoom.images.length;
	}
	function nextImage() {
		if (!galleryRoom) return;
		galleryIndex = (galleryIndex + 1) % galleryRoom.images.length;
	}

	function openDetail(room: Room) {
		detailRoom = room;
	}
	function closeDetail() {
		detailRoom = null;
	}

	function handleGalleryKeydown(e: KeyboardEvent) {
		if (e.key === 'ArrowLeft') prevImage();
		else if (e.key === 'ArrowRight') nextImage();
		else if (e.key === 'Escape') closeGallery();
	}
	function handleDetailKeydown(e: KeyboardEvent) {
		if (e.key === 'Escape') closeDetail();
	}

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

<section id="rooms" class="relative bg-card py-24">
	<div class="container mx-auto px-6">
		<div use:inview={() => (headerVisible = true)} class="mx-auto mb-16 max-w-3xl text-center">
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
						Apartamencik i 3 niezależne pokoje - każdy z osobnym wejściem, przytulnie urządzony i
						wyposażony we wszystko, czego potrzebujesz na wakacyjny wypoczynek.
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
							class="relative aspect-video w-full cursor-pointer overflow-hidden rounded-t-2xl"
							onclick={() => openGallery(room)}
						>
							<EnhancedImage
								src={room.thumbnail}
								alt={room.name}
								className="h-full w-full object-cover transition-transform duration-700 group-hover:scale-110"
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
							<div class="mb-4">
								<h3 class="mb-3 font-display text-2xl font-semibold text-foreground">
									{room.name}
								</h3>
								<div
									class="mb-4 inline-flex items-center rounded-full border border-primary/20 bg-primary/10 px-3 py-1.5 text-xs font-semibold tracking-[0.2em] text-primary uppercase"
								>
									{room.subtitle}
								</div>
								<p class="text-base leading-relaxed text-muted-foreground">
									{room.shortDescription}
								</p>
							</div>

							<div class="mb-4 flex flex-wrap gap-2">
								{#each room.keyFeatures as feature, i (i)}
									<div class="flex items-center gap-2 rounded-full bg-muted px-3 py-1.5 text-sm">
										<feature.icon class="h-4 w-4 text-primary" />
										<span class="text-foreground/80">{feature.text}</span>
									</div>
								{/each}
							</div>

							<div class="mb-5 flex flex-wrap gap-1.5">
								{#each room.equipment.slice(0, 4) as item, i (i)}
									<span
										class="rounded-md border border-border bg-background px-2.5 py-1 text-xs text-muted-foreground"
									>
										{item}
									</span>
								{/each}
								{#if room.equipment.length > 4}
									<span
										class="rounded-md border border-primary/20 bg-primary/10 px-2.5 py-1 text-xs font-medium text-primary"
									>
										+{room.equipment.length - 4} więcej
									</span>
								{/if}
							</div>

							<div class="flex gap-3">
								<a
									href="#contact"
									class="bg-gradient-sea flex-1 rounded-full px-6 py-3 text-center font-medium text-primary-foreground transition-all duration-300 hover:scale-[102%] hover:shadow-glow"
								>
									Zarezerwuj
								</a>
								<button
									type="button"
									onclick={() => openDetail(room)}
									class="flex cursor-pointer items-center gap-2 rounded-full bg-muted px-5 py-3 font-medium text-foreground transition-all duration-300 hover:bg-muted/70"
								>
									<Info class="h-4 w-4" />
									Więcej
								</button>
							</div>
						</div>
					</article>
				{/if}
			{/each}
		</div>
	</div>
</section>

{#if detailRoom}
	<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
	<div
		role="dialog"
		aria-modal="true"
		tabindex="-1"
		transition:fade={{ duration: 200 }}
		class="fixed inset-0 z-40 flex items-center justify-center bg-foreground/60 p-4 backdrop-blur-sm"
		onclick={closeDetail}
		onkeydown={handleDetailKeydown}
	>
		<div
			transition:scale={{ start: 0.95, duration: 300 }}
			class="relative max-h-[90vh] w-full max-w-2xl overflow-y-auto rounded-2xl bg-card shadow-medium"
			onclick={(e) => e.stopPropagation()}
			onkeydown={(e) => e.stopPropagation()}
			role="document"
		>
			<button
				type="button"
				class="relative aspect-video w-full cursor-pointer overflow-hidden rounded-t-2xl"
				onclick={() => {
					if (detailRoom) {
						const room = detailRoom;
						closeDetail();
						openGallery(room);
					}
				}}
			>
				<EnhancedImage
					src={detailRoom.thumbnail}
					alt={detailRoom.name}
					className="h-full w-full object-cover"
				/>
				<div
					class="absolute inset-0 bg-linear-to-t from-foreground/50 via-transparent to-transparent"
				></div>
				<div class="absolute bottom-4 left-6">
					<h3 class="font-display text-3xl font-semibold text-primary-foreground drop-shadow-lg">
						{detailRoom.name}
					</h3>
					<p class="font-body text-primary-foreground/80 drop-shadow-md">
						{detailRoom.subtitle}
					</p>
				</div>
				<div
					class="absolute right-6 bottom-4 rounded-full bg-card/80 px-4 py-2 text-sm font-medium text-foreground backdrop-blur-sm"
				>
					📷 {detailRoom.images.length} zdjęć
				</div>
			</button>

			<div class="p-6">
				<p class="mb-6 font-body leading-relaxed text-muted-foreground">
					{detailRoom.fullDescription}
				</p>

				<h4 class="mb-3 font-display text-lg font-semibold text-foreground">Wyposażenie</h4>
				<div class="mb-6 flex flex-wrap gap-2">
					{#each detailRoom.equipment as item, i (i)}
						<span
							class="rounded-lg border border-border bg-muted px-3 py-1.5 text-sm font-medium text-foreground/80"
						>
							{item}
						</span>
					{/each}
				</div>

				<div class="flex gap-3">
					<a
						href="#contact"
						onclick={closeDetail}
						class="bg-gradient-sea flex-1 rounded-full px-6 py-3 text-center font-medium text-primary-foreground transition-all duration-300 hover:shadow-glow"
					>
						Zarezerwuj
					</a>
					<button
						type="button"
						onclick={() => {
							if (detailRoom) {
								const room = detailRoom;
								closeDetail();
								openGallery(room);
							}
						}}
						class="cursor-pointer rounded-full bg-muted px-6 py-3 font-medium text-foreground transition-all duration-300 hover:bg-muted/80"
					>
						Galeria
					</button>
				</div>
			</div>

			<button
				type="button"
				onclick={closeDetail}
				class="absolute top-4 right-4 rounded-full bg-card/80 p-2 backdrop-blur-sm transition-colors hover:bg-card"
			>
				<X class="h-5 w-5 text-foreground" />
			</button>
		</div>
	</div>
{/if}

{#if galleryRoom}
	<!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
	<div
		role="dialog"
		aria-modal="true"
		tabindex="-1"
		transition:fade={{ duration: 200 }}
		class="fixed inset-0 z-50 flex items-center justify-center bg-foreground/90 p-4 backdrop-blur-md"
		onclick={closeGallery}
		onkeydown={handleGalleryKeydown}
	>
		<button
			type="button"
			onclick={closeGallery}
			class="absolute top-6 right-6 p-2 text-card transition-colors hover:text-primary"
		>
			<X class="h-8 w-8" />
		</button>

		<div
			class="relative aspect-video w-full max-w-5xl"
			onclick={(e) => e.stopPropagation()}
			onkeydown={(e) => e.stopPropagation()}
			role="document"
		>
			{#key galleryIndex}
				<EnhancedImage
					src={galleryRoom.images[galleryIndex]}
					alt={`${galleryRoom.name} - zdjęcie ${galleryIndex + 1}`}
					className="h-full w-full rounded-lg object-contain"
				/>
			{/key}

			{#if galleryRoom.images.length > 1}
				<button
					type="button"
					onclick={prevImage}
					class="absolute top-1/2 left-4 -translate-y-1/2 rounded-full bg-card/80 p-3 transition-colors hover:bg-card"
				>
					<ChevronLeft class="h-6 w-6 text-foreground" />
				</button>
				<button
					type="button"
					onclick={nextImage}
					class="absolute top-1/2 right-4 -translate-y-1/2 rounded-full bg-card/80 p-3 transition-colors hover:bg-card"
				>
					<ChevronRight class="h-6 w-6 text-foreground" />
				</button>
			{/if}

			<div class="absolute bottom-4 left-1/2 flex -translate-x-1/2 gap-2">
				{#each galleryRoom.images as _, i (i)}
					<button
						type="button"
						onclick={() => (galleryIndex = i)}
						aria-label={'Zdjęcie ' + (i + 1)}
						class="h-2 rounded-full transition-all {i === galleryIndex
							? 'w-6 bg-primary'
							: 'w-2 bg-card/60'}"
					></button>
				{/each}
			</div>

			<div
				class="absolute top-4 left-1/2 -translate-x-1/2 rounded-full bg-card/80 px-4 py-1.5 text-sm font-medium text-foreground backdrop-blur-sm"
			>
				{galleryIndex + 1} / {galleryRoom.images.length}
			</div>
		</div>
	</div>
{/if}
