<script lang="ts">
	/* eslint-disable svelte/no-navigation-without-resolve */
	import { fade, fly } from 'svelte/transition';
	import { MapPin, Phone, Mail, Clock, Send } from '@lucide/svelte';
	import { z } from 'zod';

	const contactFormSchema = z.object({
		name: z.string().trim().min(2, { message: 'Imię musi mieć co najmniej 2 znaki' }).max(100),
		email: z.string().trim().email({ message: 'Nieprawidłowy adres e-mail' }).max(255),
		phone: z.string().trim().max(30).optional().or(z.literal('')),
		message: z
			.string()
			.trim()
			.min(10, { message: 'Wiadomość musi mieć co najmniej 10 znaków' })
			.max(1000)
	});

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

	let formData = { name: '', email: '', phone: '', message: '' };
	let isSubmitting = false;
	let isInView = false;
	let errorMessage = '';
	let successMessage = '';
	let contactSection: boolean | HTMLElement = false;

	const handleSubmit = (e: Event) => {
		e.preventDefault();
		errorMessage = '';
		successMessage = '';

		const result = contactFormSchema.safeParse(formData);
		if (!result.success) {
			errorMessage = result.error.issues[0].message;
			return;
		}

		isSubmitting = true;
		const subject = encodeURIComponent(`Zapytanie od ${result.data.name}`);
		const body = encodeURIComponent(
			`Imię i nazwisko: ${result.data.name}\nE-mail: ${result.data.email}\nTelefon: ${result.data.phone || '-'}\n\nWiadomość:\n${result.data.message}`
		);
		window.location.href = `mailto:rezerwacje@plazablisko.pl?subject=${subject}&body=${body}`;

		setTimeout(() => {
			isSubmitting = false;
			successMessage = 'Dziękujemy! Otworzyliśmy Twojego klienta poczty z gotową wiadomością.';
			formData = { name: '', email: '', phone: '', message: '' };
		}, 500);
	};

	function checkInView() {
		if (!contactSection) return;
		const rect = contactSection.getBoundingClientRect();
		isInView = rect.top < window.innerHeight - 100;
	}
</script>

<svelte:window on:scroll={checkInView} />

<section id="contact" class="bg-gradient-sand relative overflow-hidden py-24">
	<div class="absolute top-0 right-0 h-96 w-96 rounded-full bg-primary/5 blur-3xl"></div>
	<div class="absolute bottom-0 left-0 h-64 w-64 rounded-full bg-sunset/5 blur-3xl"></div>

	<div class="relative z-10 container mx-auto px-6" bind:this={contactSection}>
		<div class="mx-auto mb-16 max-w-3xl text-center" transition:fade={{ duration: 600 }}>
			<span class="mb-4 inline-block text-sm font-medium tracking-widest text-primary uppercase">
				Kontakt
			</span>
			<h2 class="mb-6 font-display text-4xl font-semibold text-foreground md:text-5xl">
				Zarezerwuj pobyt
			</h2>
			<p class="font-body text-lg leading-relaxed text-muted-foreground">
				Masz pytania? Chcesz zarezerwować pokój? Skontaktuj się z nami telefonicznie lub mailowo. Z
				przyjemnością odpowiemy na wszystkie pytania.
			</p>
		</div>

		<div class="grid items-stretch gap-8 lg:grid-cols-2">
			<div
				class="grid auto-rows-fr gap-4 sm:grid-cols-2"
				transition:fly={{ x: -30, duration: 600, delay: 200 }}
			>
				{#each contactInfo as item, index (index)}
					<div
						class="group rounded-2xl bg-card p-6 shadow-soft transition-all duration-300 hover:shadow-medium"
						transition:fly={{ y: 20, duration: 500, delay: 300 + index * 100 }}
					>
						<div
							class="bg-gradient-sea mb-4 flex h-12 w-12 items-center justify-center rounded-xl transition-transform duration-300 group-hover:scale-110"
						>
							<svelte:component this={item.icon} class="h-6 w-6 text-primary-foreground" />
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
				{/each}
			</div>

			<div
				class="flex flex-col rounded-2xl bg-card p-8 shadow-medium"
				transition:fly={{ x: 30, duration: 600, delay: 400 }}
			>
				<h3 class="mb-4 font-display text-2xl font-semibold text-foreground">
					Formularz kontaktowy
				</h3>
				<p class="mb-6 font-body text-muted-foreground">
					Wypełnij formularz – odezwiemy się najszybciej jak to możliwe i pomożemy w wyborze
					idealnego pokoju.
				</p>

				<form on:submit={handleSubmit} class="flex flex-1 flex-col space-y-4">
					{#if errorMessage}
						<div class="rounded-lg bg-red-50 p-3 text-sm text-red-600">
							{errorMessage}
						</div>
					{/if}

					{#if successMessage}
						<div class="rounded-lg bg-green-50 p-3 text-sm text-green-600">
							{successMessage}
						</div>
					{/if}

					<div>
						<label for="name" class="mb-1 block text-sm font-medium text-foreground">
							Imię i nazwisko *
						</label>
						<input
							id="name"
							type="text"
							bind:value={formData.name}
							maxlength="100"
							required
							class="w-full rounded-xl border border-input bg-background px-4 py-3 text-foreground transition focus:ring-2 focus:ring-primary/40 focus:outline-none"
						/>
					</div>

					<div class="grid gap-4 sm:grid-cols-2">
						<div>
							<label for="email" class="mb-1 block text-sm font-medium text-foreground">
								E-mail *
							</label>
							<input
								id="email"
								type="email"
								bind:value={formData.email}
								maxlength="255"
								required
								class="w-full rounded-xl border border-input bg-background px-4 py-3 text-foreground transition focus:ring-2 focus:ring-primary/40 focus:outline-none"
							/>
						</div>
						<div>
							<label for="phone" class="mb-1 block text-sm font-medium text-foreground">
								Telefon
							</label>
							<input
								id="phone"
								type="tel"
								bind:value={formData.phone}
								maxlength="30"
								class="w-full rounded-xl border border-input bg-background px-4 py-3 text-foreground transition focus:ring-2 focus:ring-primary/40 focus:outline-none"
							/>
						</div>
					</div>

					<div class="flex flex-1 flex-col">
						<label for="message" class="mb-1 block text-sm font-medium text-foreground">
							Wiadomość *
						</label>
						<textarea
							id="message"
							bind:value={formData.message}
							maxlength="1000"
							required
							class="min-h-30 w-full flex-1 resize-none rounded-xl border border-input bg-background px-4 py-3 text-foreground transition focus:ring-2 focus:ring-primary/40 focus:outline-none"
						></textarea>
					</div>

					<button
						type="submit"
						disabled={isSubmitting}
						class="bg-gradient-sea flex items-center justify-center gap-3 rounded-full px-6 py-4 font-medium text-primary-foreground shadow-soft transition-all duration-300 hover:scale-105 hover:shadow-glow disabled:opacity-60 disabled:hover:scale-100"
					>
						<Send class="h-5 w-5" />
						<span>{isSubmitting ? 'Wysyłanie...' : 'Wyślij wiadomość'}</span>
					</button>
				</form>
			</div>
		</div>

		<div
			class="mt-12 h-80 overflow-hidden rounded-2xl shadow-medium md:h-96"
			transition:fade={{ duration: 600, delay: 500 }}
		>
			<iframe
				src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d2334.7616755682047!2d15.578212!3d54.1842965!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x4700159b344bcf89%3A0x86a8c03659866bcf!2splazablisko.pl!5e0!3m2!1spl!2spl!4v1779701596098!5m2!1spl!2spl"
				width="100%"
				title="Lokalizacja Plaza Blisko"
				height="100%"
				style="border:0;"
				loading="lazy"
				referrerpolicy="no-referrer-when-downgrade"
			></iframe>
		</div>
	</div>
</section>
