<script lang="ts">
	/* eslint-disable svelte/no-navigation-without-resolve */
	import { fade, fly } from 'svelte/transition';
	import { writable } from 'svelte/store';
	import { MapPin, Phone, Mail, Clock, Send } from '@lucide/svelte';
	import emailjs from '@emailjs/browser';

	emailjs.init('Yf4SNVhJSYCRpvnH7');

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
	let lastSent = 0;
	let errors: { [key: string]: string } = {};
	let isSubmitting = false;
	const toastMessage = writable<string | null>(null);
	let contactSection: HTMLElement | null = null;

	const canSend = () => {
		const now = Date.now();
		if (now - lastSent < 10000) {
			alert('Poczekaj chwilę przed ponownym wysłaniem.');
			return false;
		}
		lastSent = now;
		return true;
	};

	const validate = () => {
		const newErrors: { [key: string]: string } = {};
		if (!formData.name.trim()) {
			newErrors.name = 'Imię i nazwisko są wymagane.';
		}
		if (!formData.email.trim()) {
			newErrors.email = 'Email jest wymagany.';
		} else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email)) {
			newErrors.email = 'Nieprawidłowy format email.';
		}
		if (!formData.message.trim()) {
			newErrors.message = 'Wiadomość jest wymagana.';
		}
		return newErrors;
	};

	const showToast = (message: string) => {
		toastMessage.set(message);
		setTimeout(() => toastMessage.set(null), 5000);
	};

	const handleSubmit = async (e: Event) => {
		e.preventDefault();
		if (!canSend()) return;

		errors = validate();
		if (Object.keys(errors).length > 0) {
			return;
		}

		isSubmitting = true;
		try {
			await emailjs.send(
				'service_bl5857h',
				'template_icf1qgr',
				{
					title: 'Formularz kontaktowy ze strony',
					name: formData.name,
					email: formData.email,
					phone: formData.phone,
					message: formData.message
				},
				'TMUBH_SBSZY1QNwXK'
			);
			showToast('Wiadomość wysłana! Skontaktujemy się z Tobą wkrótce.');
			formData = { name: '', email: '', phone: '', message: '' };
			errors = {};
		} catch {
			showToast('Wystąpił błąd podczas wysyłania wiadomości. Spróbuj ponownie.');
		} finally {
			isSubmitting = false;
		}
	};

	const handleInput = (field: keyof typeof formData, value: string) => {
		formData = { ...formData, [field]: value };
		if (errors[field]) {
			const { [field]: removed, ...rest } = errors;
			void removed;
			errors = rest;
		}
	};
</script>

<section id="contact" class="bg-gradient-sand relative overflow-hidden py-24">
	<div class="absolute top-0 right-0 h-96 w-96 rounded-full bg-primary/5 blur-3xl"></div>
	<div class="absolute bottom-0 left-0 h-64 w-64 rounded-full bg-sunset/5 blur-3xl"></div>

	<div class="relative z-10 container mx-auto px-6" bind:this={contactSection}>
		{#if $toastMessage}
			<div class="fixed inset-x-0 bottom-6 z-50 flex justify-center px-4">
				<div
					class="rounded-full bg-foreground/95 px-6 py-3 text-sm text-background shadow-xl backdrop-blur-md transition duration-300"
					transition:fade={{ duration: 200 }}
				>
					{$toastMessage}
				</div>
			</div>
		{/if}
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
					<div>
						<label for="name" class="mb-1 block text-sm font-medium text-foreground">
							Imię i nazwisko *
						</label>
						<input
							id="name"
							type="text"
							value={formData.name}
							on:input={(e) => handleInput('name', e.currentTarget.value)}
							maxlength="100"
							required
							class="w-full rounded-xl border border-input bg-background px-4 py-3 text-foreground transition focus:ring-2 focus:ring-primary/40 focus:outline-none"
						/>
						{#if errors.name}
							<p class="mt-1 text-sm text-red-600">{errors.name}</p>
						{/if}
					</div>

					<div class="grid gap-4 sm:grid-cols-2">
						<div>
							<label for="email" class="mb-1 block text-sm font-medium text-foreground">
								E-mail *
							</label>
							<input
								id="email"
								type="email"
								value={formData.email}
								on:input={(e) => handleInput('email', e.currentTarget.value)}
								maxlength="255"
								required
								class="w-full rounded-xl border border-input bg-background px-4 py-3 text-foreground transition focus:ring-2 focus:ring-primary/40 focus:outline-none"
							/>
							{#if errors.email}
								<p class="mt-1 text-sm text-red-600">{errors.email}</p>
							{/if}
						</div>
						<div>
							<label for="phone" class="mb-1 block text-sm font-medium text-foreground">
								Telefon
							</label>
							<input
								id="phone"
								type="tel"
								value={formData.phone}
								on:input={(e) => handleInput('phone', e.currentTarget.value)}
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
							value={formData.message}
							on:input={(e) => handleInput('message', e.currentTarget.value)}
							maxlength="1000"
							required
							class="min-h-30 w-full flex-1 resize-none rounded-xl border border-input bg-background px-4 py-3 text-foreground transition focus:ring-2 focus:ring-primary/40 focus:outline-none"
						></textarea>
						{#if errors.message}
							<p class="mt-1 text-sm text-red-600">{errors.message}</p>
						{/if}
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
