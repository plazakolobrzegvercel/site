<script lang="ts">
	import { fly } from 'svelte/transition';
	import { MapPin, Phone, Mail, Clock, Send } from '@lucide/svelte';

	const contactInfo = [
		{
			icon: MapPin,
			title: 'Adres',
			content: 'ul. Kopernika 7/1',
			subContent: '78-100 Kołobrzeg'
		},
		{
			icon: Phone,
			title: 'Telefon',
			content: '502 258 401',
			href: 'tel:+48502258401'
		},
		{
			icon: Mail,
			title: 'E-mail',
			content: 'rezerwacje@plazablisko.pl',
			href: 'mailto:rezerwacje@plazablisko.pl'
		},
		{
			icon: Clock,
			title: 'Zameldowanie',
			content: 'od 14:00',
			subContent: 'Wymeldowanie do 10:00'
		}
	];

	let headerVisible = $state(false);
	let infoVisible = $state(false);
	let formVisible = $state(false);

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

<section id="contact" class="bg-gradient-sand relative overflow-hidden py-24">
	<div class="absolute top-0 right-0 h-96 w-96 rounded-full bg-primary/5 blur-3xl"></div>
	<div class="absolute bottom-0 left-0 h-64 w-64 rounded-full bg-sunset/5 blur-3xl"></div>

	<div class="relative z-10 container mx-auto max-w-350 px-6">
		<div use:inview={() => (headerVisible = true)} class="mx-auto mb-16 max-w-3xl text-center">
			{#if headerVisible}
				<div transition:fly={{ y: 30, duration: 600 }}>
					<span
						class="mb-4 inline-block text-sm font-medium tracking-widest text-primary uppercase"
					>
						Kontakt
					</span>
					<h2 class="mb-6 font-display text-4xl font-semibold text-foreground md:text-5xl">
						Zarezerwuj pobyt
					</h2>
					<p class="font-body text-lg leading-relaxed text-muted-foreground">
						Masz pytania? Chcesz zarezerwować pokój? Skontaktuj się z nami telefonicznie lub
						mailowo. Z przyjemnością odpowiemy na wszystkie pytania.
					</p>
				</div>
			{/if}
		</div>

		<div class="grid items-start gap-12 lg:grid-cols-2">
			<div use:inview={() => (infoVisible = true)} class="grid gap-4 sm:grid-cols-2">
				{#each contactInfo as item, index (item.title)}
					{#if infoVisible}
						<div
							transition:fly={{ y: 20, duration: 500, delay: 200 + index * 100 }}
							class="group rounded-2xl bg-card p-6 shadow-soft transition-all duration-300 hover:shadow-medium"
						>
							<div
								class="bg-gradient-sea mb-4 flex h-12 w-12 items-center justify-center rounded-xl transition-transform duration-300 group-hover:scale-110"
							>
								<item.icon class="h-6 w-6 text-primary-foreground" />
							</div>
							<h3 class="mb-2 font-display text-lg font-semibold text-foreground">
								{item.title}
							</h3>
							{#if item.href}
								<a
									href={item.href}
									class="font-body text-muted-foreground transition-colors hover:text-primary"
								>
									{item.content}
								</a>
							{:else}
								<p class="font-body text-muted-foreground">{item.content}</p>
								{#if item.subContent}
									<p class="mt-1 font-body text-sm text-muted-foreground">
										{item.subContent}
									</p>
								{/if}
							{/if}
						</div>
					{/if}
				{/each}
			</div>

			<div use:inview={() => (formVisible = true)} class="contents">
				<div
					transition:fly={{ x: 30, duration: 600, delay: 400 }}
					class="rounded-2xl bg-card p-8 shadow-medium"
				>
					<h2 class="mb-4 font-display text-2xl font-semibold text-foreground">
						Szybka rezerwacja
					</h2>
					<p class="mb-6 font-body text-muted-foreground">
						Zadzwoń do nas lub napisz email - odpowiemy najszybciej jak to możliwe i pomożemy w
						wyborze idealnego pokoju na Twój wypoczynek.
					</p>

					<div class="space-y-4">
						<a
							href="tel:+48502258401"
							class="bg-gradient-sea flex w-full items-center justify-center gap-3 rounded-full px-6 py-4 font-medium text-primary-foreground shadow-soft transition-all duration-300 hover:scale-105 hover:shadow-glow"
						>
							<Phone class="h-5 w-5" />
							<span>Zadzwoń: 502 258 401</span>
						</a>

						<a
							href="mailto:rezerwacje@plazablisko.pl"
							class="flex w-full items-center justify-center gap-3 rounded-full border-2 border-primary/20 bg-background px-6 py-4 font-medium text-foreground transition-all duration-300 hover:scale-105 hover:border-primary/40"
						>
							<Send class="h-5 w-5 text-primary" />
							<span>Napisz email</span>
						</a>
					</div>

					<div class="mt-8 h-48 overflow-hidden rounded-xl bg-muted">
						<iframe
							src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2355.0123456789!2d15.576789!3d54.177654!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47002f8b6a7c5f89%3A0x1234567890abcdef!2sul.%20Kopernika%207%2F1%2C%2078-100%20Ko%C5%82obrzeg!5e0!3m2!1spl!2spl!4v1234567890123"
							width="100%"
							height="100%"
							allowfullscreen
							loading="lazy"
							referrerpolicy="no-referrer-when-downgrade"
							title="Lokalizacja Plaza Blisko"
						></iframe>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>
