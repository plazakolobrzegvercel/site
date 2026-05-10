<script>
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import { fade } from 'svelte/transition';
	import {
		ArrowLeft,
		FileText,
		ScrollText,
		MapPin,
		Phone,
		Mail,
		Heart,
		Waves
	} from '@lucide/svelte';
	import logo from '$lib/assets/logo.avif';
	import buildingImg from '$lib/assets/building.avif';
	import EnhancedImage from '$lib/components/EnhancedImage.svelte';

	const regulations = [
		'W celu potwierdzenia rezerwacji należy wpłacić uzgodniony zadatek na rachunek mBank 30 1140 2004 0000 3302 7770 2237. Domyślnie jest to kwota 30% wartości rezerwacji.',
		'Doba hotelowa rozpoczyna się o godzinie 15:00, a kończy się o godzinie 10:00 ostatniego dnia pobytu. Jeśli chcesz przyjechać wcześniej lub zostać dłużej, uzgodnij to wcześniej z nami. Należność za pobyt oraz opłata klimatyczna pobierana jest w dniu przyjazdu. Jeśli chcesz wyjechać wcześniej niż wynika to z rezerwacji, opłata nie ulega zmianie.',
		'Nie możesz przekazać pokoju innym osobom, nawet jeśli nie upłynął okres, za który uiściłeś należną za pobyt opłatę.',
		'W przypadku niezrealizowanego pobytu zadatek przepada w całości.',
		'Nie ponosimy odpowiedzialności za rzeczy wartościowe oraz pieniądze pozostawione w pokojach. Nie ponosimy odpowiedzialności za uszkodzenia czy utratę samochodu czy innego pojazdu. Udostępniamy parking, ryzyko jest po stronie gościa.',
		'Po uzgodnieniu z nami możesz zaparkować swój samochód na miejscu przez nas wskazanym. Parking dostępny jest wyłącznie dla gości, którzy opłacili pobyt.',
		'Jako nasz Gość ponosisz pełną odpowiedzialność materialną za wszelkiego rodzaju uszkodzenia lub zniszczenia przedmiotów wyposażenia i urządzeń technicznych powstałe z Twojej winy lub z winy osób Ci towarzyszących.',
		'W pokojach nie może przebywać większa ilość osób niż wynika to z rezerwacji.',
		'Wszystkie usterki zgłaszaj niezwłocznie pod nr tel. 502 258 401.',
		'Nie wolno podłączać urządzeń elektrycznych nie będących na wyposażeniu pokoju, takich jak grzałki, mikrofalówki, frytkownice, gofrownice, kuchenki elektryczne i inne tego typu. Nie wolno używać kuchenek gazowych. Można używać ładowarek do urządzeń typu telefon, laptop, aparat fotograficzny. Wszystko to ze względów bezpieczeństwa przeciwpożarowego.',
		'Osobom postronnym nie udzielamy żadnych informacji o danych osobowych gości.',
		'We wszystkich pomieszczeniach NIE WOLNO PALIĆ papierosów, e-papierosów ani innych wyrobów tytoniowych. Na dymka zapraszamy do ogródka – przy stoliku znajdziesz doniczkę na popioły.',
		'Po upływie terminu pobytu masz obowiązek oddać nam klucze. Przed wyjazdem sprawdzimy stan pokoju i w razie uszkodzeń lub silnych zabrudzeń obciążymy kosztami naprawy lub sprzątania.',
		'Z chwilą stwierdzenia nieprzestrzegania regulaminu mamy prawo do natychmiastowego wypowiedzenia pobytu bez zwrotu pieniędzy.',
		'Cisza nocna obowiązuje od godziny 22:00 do 6:00 rano.',
		'Rezerwując pobyt, zobowiązujesz się do przestrzegania powyższego regulaminu.'
	];

	onMount(() => {
		if ($page.url.hash) {
			const id = $page.url.hash.replace('#', '');
			const el = document.getElementById(id);
			if (el) {
				setTimeout(() => el.scrollIntoView({ behavior: 'smooth', block: 'start' }), 100);
				return;
			}
		}
		window.scrollTo(0, 0);
	});

	const currentYear = new Date().getFullYear();
</script>

<svelte:head>
	<title>Plaza Blisko - Informacje i regulamin</title>
</svelte:head>

<div class="min-h-screen bg-background">
	<header class="sticky top-0 z-50 bg-primary py-4 shadow-medium">
		<div class="container mx-auto flex items-center justify-between gap-6 px-6">
			<a href="/" class="flex items-center gap-3">
				<EnhancedImage
					src={logo}
					alt="Plaza Blisko"
					className="h-12 w-auto"
					width={200}
					height={60}
				/>
			</a>
			<ul class="hidden items-center gap-8 md:flex">
				<li>
					<a
						href="/#home"
						class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
					>
						Start
						<span
							class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
						/>
					</a>
				</li>
				<li>
					<a
						href="/#about"
						class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
					>
						O nas
						<span
							class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
						/>
					</a>
				</li>
				<li>
					<a
						href="/#rooms"
						class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
					>
						Pokoje
						<span
							class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
						/>
					</a>
				</li>
				<li>
					<a
						href="/#contact"
						class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
					>
						Kontakt
						<span
							class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
						/>
					</a>
				</li>
				<li>
					<a
						href="#regulamin"
						class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
					>
						Regulamin
						<span
							class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
						/>
					</a>
				</li>
				<li>
					<a
						href="/#contact"
						class="rounded-full bg-card px-6 py-2.5 text-sm font-medium text-foreground shadow-soft transition-all duration-300 hover:scale-105 hover:shadow-medium"
					>
						Rezerwacja
					</a>
				</li>
			</ul>
			<a
				href="/"
				class="flex items-center gap-2 rounded-full bg-card px-4 py-2 text-sm font-medium text-foreground shadow-soft md:hidden"
			>
				<ArrowLeft class="h-4 w-4" />
				Strona główna
			</a>
		</div>
	</header>
	<section class="bg-gradient-sea relative overflow-hidden py-20">
		<div class="absolute inset-0 bg-primary/20" />
		<div class="relative z-10 container mx-auto px-6">
			<div class="mx-auto max-w-3xl text-center" transition:fade={{ duration: 600 }}>
				<span
					class="mb-4 inline-block text-sm font-medium tracking-widest text-primary-foreground/80 uppercase"
				>
					Poznaj nas bliżej
				</span>
				<h1
					class="mb-6 font-display text-4xl font-semibold text-primary-foreground md:text-5xl lg:text-6xl"
				>
					Informacje i regulamin
				</h1>
				<p class="font-body text-lg leading-relaxed text-primary-foreground/80">
					Wszystko, co warto wiedzieć przed przyjazdem do naszego domku w Kołobrzegu.
				</p>
			</div>
		</div>
	</section>

	<section class="bg-card py-20">
		<div class="container mx-auto px-6">
			<div class="grid items-center gap-12 lg:grid-cols-2">
				<div transition:fade={{ duration: 600 }}>
					<span
						class="mb-4 inline-block text-sm font-medium tracking-widest text-primary uppercase"
					>
						O nas
					</span>
					<h2 class="mb-6 font-display text-3xl font-semibold text-foreground md:text-4xl">
						Plaża blisko – to nie tylko nazwa
					</h2>
					<div class="space-y-4 font-body leading-relaxed text-muted-foreground">
						<p>
							Jedna z naszych gościń, gdy przyjechała do nas po raz pierwszy, powiedziała:
							<em class="font-medium text-foreground">
								„Myślałam, że plaża blisko to taki chwyt marketingowy, ale tutaj naprawdę jest
								wszędzie blisko! Blisko do plaży, blisko do dworca, blisko do centrum miasta."
							</em>
						</p>
						<p>
							I dokładnie tak jest. Nasz domek na ul. Kopernika w Kołobrzegu leży zaledwie 100
							metrów od piaszczystej plaży, w spokojnej dzielnicy uzdrowiskowej. Tuż obok biegnie
							najdłuższa w Polsce aleja nadmorska – Promenada Morskich Szeptów. To miejsce, gdzie
							morski powiew towarzyszy Ci od rana do wieczora.
						</p>
						<p>
							Oferujemy apartamencik i 3 niezależne pokoje – każdy z osobnym wejściem, żebyś mógł
							czuć się swobodnie i wracać kiedy zechcesz. Dbamy o czystość osobiście, a przed każdym
							przyjazdem ozonujemy pomieszczenia. Ceny ustalamy indywidualnie, zależnie od terminu i
							długości pobytu – zawsze warto zapytać.
						</p>
					</div>
				</div>

				<div class="relative" transition:fade={{ duration: 600, delay: 200 }}>
					<div class="overflow-hidden rounded-2xl shadow-medium">
						<EnhancedImage
							src={buildingImg}
							alt="Domek Plaza Blisko w Kołobrzegu"
							className="h-auto w-full object-cover"
						/>
					</div>
					<div
						class="absolute -bottom-4 -left-4 rounded-xl bg-primary px-6 py-3 text-primary-foreground shadow-medium"
					>
						<div class="flex items-center gap-2">
							<MapPin class="h-5 w-5" />
							<span class="font-display font-semibold">100m od plaży</span>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<section class="bg-background py-16">
		<div class="container mx-auto px-6">
			<div class="grid items-center gap-12 lg:grid-cols-2">
				<div transition:fade={{ duration: 600 }}>
					<div class="mb-6 inline-flex items-center gap-2 rounded-full bg-primary/10 px-4 py-2">
						<FileText class="h-5 w-5 text-primary" />
						<span class="text-sm font-medium text-primary">Dokument urzędowy</span>
					</div>
					<h2 class="mb-6 font-display text-3xl font-semibold text-foreground md:text-4xl">
						Zaświadczenie
					</h2>
					<p class="font-body leading-relaxed text-muted-foreground">
						Nasz obiekt jest oficjalnie zgłoszony i figuruje w ewidencji obiektów świadczących
						usługi hotelarskie prowadzonej przez Urząd Miasta Kołobrzeg.
					</p>
				</div>

				<div
					class="overflow-hidden rounded-2xl shadow-medium"
					transition:fade={{ duration: 600, delay: 200 }}
				>
					<EnhancedImage
						src="https://plazablisko.pl/wp-content/uploads/2020/08/zaswiadczenie-img.jpg"
						alt="Zaświadczenie o wpisie do ewidencji obiektów hotelarskich"
						className="h-auto w-full"
					/>
				</div>
			</div>
		</div>
	</section>

	<section id="regulamin" class="scroll-mt-24 bg-card py-20">
		<div class="container mx-auto px-6">
			<div class="mx-auto mb-12 max-w-3xl text-center" transition:fade={{ duration: 600 }}>
				<div class="mb-6 inline-flex items-center gap-2 rounded-full bg-primary/10 px-4 py-2">
					<ScrollText class="h-5 w-5 text-primary" />
					<span class="text-sm font-medium text-primary">Regulamin</span>
				</div>
				<h2 class="mb-4 font-display text-3xl font-semibold text-foreground md:text-4xl">
					Regulamin wynajmu pokoi
				</h2>
				<p class="font-body leading-relaxed text-muted-foreground">
					Podstawowe zasady obowiązujące w naszym domku na ul. Kopernika 7/1 w Kołobrzegu. Prosimy o
					zapoznanie się przed rezerwacją.
				</p>
			</div>

			<div class="mx-auto max-w-3xl">
				<div class="space-y-4">
					{#each regulations as item, index (index)}
						<div
							class="flex gap-4 rounded-xl border border-border bg-background p-4 transition-colors hover:border-primary/30"
							transition:fade={{ duration: 400, delay: index * 30 }}
						>
							<span
								class="flex h-8 w-8 shrink-0 items-center justify-center rounded-full bg-primary/10 font-display text-sm font-semibold text-primary"
							>
								{index + 1}
							</span>
							<p class="pt-1 font-body text-sm leading-relaxed text-muted-foreground">
								{item}
							</p>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</section>

	<section class="bg-gradient-sea relative overflow-hidden py-20">
		<div class="absolute inset-0 bg-primary/10"></div>
		<div class="relative z-10 container mx-auto px-6">
			<div class="mx-auto max-w-2xl text-center" transition:fade={{ duration: 600 }}>
				<h2 class="mb-6 font-display text-3xl font-semibold text-primary-foreground md:text-4xl">
					Zapraszamy do siebie!
				</h2>
				<p class="mb-10 font-body text-lg leading-relaxed text-primary-foreground/80">
					Morze, cisza i komfort czekają na wyciągnięcie ręki. Sprawdź dostępność naszych pokoi i
					zarezerwuj swój kawałek wakacji w Kołobrzegu. Chętnie odpowiemy na wszystkie pytania –
					zadzwoń lub napisz.
				</p>

				<div class="mb-10 flex flex-col justify-center gap-4 sm:flex-row">
					<a
						href="tel:+48502258401"
						class="inline-flex items-center justify-center gap-2 rounded-full bg-card px-8 py-4 font-medium text-foreground shadow-medium transition-all duration-300 hover:scale-105 hover:shadow-glow"
					>
						<Phone class="h-5 w-5" />
						502 258 401
					</a>
					<a
						href="mailto:rezerwacje@plazablisko.pl"
						class="inline-flex items-center justify-center gap-2 rounded-full border border-primary-foreground/20 bg-primary-foreground/10 px-8 py-4 font-medium text-primary-foreground transition-all duration-300 hover:bg-primary-foreground/20"
					>
						<Mail class="h-5 w-5" />
						rezerwacje@plazablisko.pl
					</a>
				</div>

				<a
					href="/"
					class="inline-flex items-center gap-2 font-medium text-primary-foreground/70 transition-colors hover:text-primary-foreground"
				>
					<ArrowLeft class="h-4 w-4" />
					Wróć na stronę główną
				</a>
			</div>
		</div>
	</section>

	<footer class="bg-primary py-8 text-primary-foreground">
		<div class="container mx-auto px-6">
			<div class="flex flex-col items-center justify-between gap-4 md:flex-row">
				<p class="flex items-center gap-2 font-body text-xs text-primary-foreground/60">
					<Waves class="h-4 w-4" />
					© {currentYear} Plaza Blisko. Wszelkie prawa zastrzeżone.
				</p>
				<p class="flex items-center gap-1 font-body text-xs text-primary-foreground/60">
					Stworzone z <Heart class="h-3 w-3 text-sunset" /> w Kołobrzegu
				</p>
			</div>
		</div>
	</footer>
</div>
