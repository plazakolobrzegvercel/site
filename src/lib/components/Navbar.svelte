<script lang="ts">
	/* eslint-disable svelte/no-navigation-without-resolve */
	import { onMount } from 'svelte';
	import { Menu, X } from '@lucide/svelte';
	import logo from '$lib/assets/logo.avif';
	import { fly } from 'svelte/transition';

	const navLinks = [
		{ href: '#home', label: 'Start' },
		{ href: '#rooms', label: 'Pokoje' },
		{ href: '#about', label: 'O nas' },
		{ href: '#contact', label: 'Kontakt' },
		{ href: '/informacje#regulamin', label: 'Regulamin', isRoute: true }
	];

	let isScrolled = false;
	let isMobileMenuOpen = false;

	const handleScroll = (hero: HTMLElement | null) => {
		if (!hero) {
			isScrolled = window.scrollY > 25;
			return;
		}

		isScrolled = hero.getBoundingClientRect().bottom <= 0;
	};

	onMount(() => {
		const hero = document.getElementById('home');

		handleScroll(hero);
		window.addEventListener('scroll', (e: Event) => handleScroll(hero), { passive: true });
		return () => window.removeEventListener('scroll', (e: Event) => handleScroll(hero));
	});
</script>

<header
	class={`fixed top-0 right-0 left-0 z-50 transition-all duration-200 ${
		isScrolled ? 'bg-primary/95 shadow-medium backdrop-blur-md ' : 'bg-primary/90 backdrop-blur-sm'
	}`}
>
	<nav
		class={`relative container mx-auto flex items-center justify-center bg-transparent px-6 transition-all duration-300 ${
			isScrolled ? 'py-6 md:py-4' : 'py-7 md:py-6'
		}`}
	>
		<a
			href="#home"
			class="absolute left-4 flex items-center gap-3 text-primary-foreground md:hidden"
		>
			<img src={logo} alt="Plaża Blisko" class="h-8 w-auto object-contain" />
		</a>

		<ul class="hidden items-center gap-8 md:flex">
			{#each navLinks as link, index (index)}
				<li>
					{#if link.isRoute}
						<a
							href={link.href}
							class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
						>
							{link.label}
							<span
								class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
							></span>
						</a>
					{:else}
						<a
							href={link.href}
							class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
						>
							{link.label}
							<span
								class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
							></span>
						</a>
					{/if}
				</li>
			{/each}
			<li>
				<a
					href="#contact"
					class="rounded-full bg-card px-6 py-2.5 text-sm font-medium text-foreground shadow-soft transition-all duration-300 hover:scale-105 hover:shadow-medium"
				>
					Rezerwacja
				</a>
			</li>
		</ul>

		<button
			on:click={() => (isMobileMenuOpen = !isMobileMenuOpen)}
			class="absolute right-4 z-10 p-4 text-primary-foreground md:hidden"
			aria-label="Toggle menu"
		>
			{#if isMobileMenuOpen}
				<X size={28} />
			{:else}
				<Menu size={28} />
			{/if}
		</button>
	</nav>

	{#if isMobileMenuOpen}
		<div class={`bg-transparent md:hidden ${isScrolled ? ' py-7  md:py-3' : ' py-8  md:py-6'}`}>
			<ul class="container mx-auto flex flex-col gap-2 bg-transparent px-6 py-2">
				{#each navLinks as link, index (index)}
					<li>
						{#if link.isRoute}
							<a
								href={link.href}
								on:click={() => (isMobileMenuOpen = false)}
								class="block py-5 font-body text-lg font-medium text-primary-foreground/90 transition-colors hover:text-primary-foreground"
							>
								{link.label}
							</a>
						{:else}
							<a
								href={link.href}
								on:click={() => (isMobileMenuOpen = false)}
								class="block py-5 font-body text-lg font-medium text-primary-foreground/90 transition-colors hover:text-primary-foreground"
							>
								{link.label}
							</a>
						{/if}
					</li>
				{/each}
				<li class="pt-2">
					<a
						href="#contact"
						on:click={() => (isMobileMenuOpen = false)}
						class="block w-full rounded-full bg-card px-6 py-5 text-center font-medium text-foreground"
					>
						Rezerwacja
					</a>
				</li>
			</ul>
		</div>
	{/if}
</header>
