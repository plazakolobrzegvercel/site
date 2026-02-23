<script lang="ts">
	import { fly, fade, slide } from 'svelte/transition';
	import { Menu, X } from '@lucide/svelte';
	import logo from '$lib/assets/logo.avif';

	const navLinks = [
		{ href: '#home', label: 'Start' },
		{ href: '#about', label: 'O nas' },
		{ href: '#rooms', label: 'Pokoje' },
		{ href: '#contact', label: 'Kontakt' }
	];

	let isScrolled = $state(false);
	let isMobileMenuOpen = $state(false);

	function handleScroll() {
		isScrolled = window.scrollY > 50;
	}
</script>

<svelte:window onscroll={handleScroll} />

<nav
	class="fixed top-0 right-0 left-0 z-50 transition-all duration-500 {isScrolled
		? 'bg-primary/95 py-3 shadow-medium backdrop-blur-md'
		: 'bg-primary/90 py-6 backdrop-blur-sm'}"
>
	<div class="container mx-auto flex max-w-350 items-center justify-between px-6">
		<a href="#home" class="relative z-10">
			<img
				src={logo}
				alt="Plaza Blisko - Pokoje Gościnne Kołobrzeg"
				class="h-14 w-auto transition-all duration-500 md:h-16 {isScrolled ? 'h-10! md:h-12!' : ''}"
			/>
		</a>

		<ul class="hidden items-center gap-8 md:flex">
			{#each navLinks as link, index (link.href)}
				<li in:fly={{ y: -20, duration: 400, delay: index * 100 }}>
					<a
						href={link.href}
						class="group relative font-body text-sm font-medium tracking-wide text-primary-foreground/90 transition-colors duration-300 hover:text-primary-foreground"
					>
						{link.label}
						<span
							class="absolute -bottom-1 left-0 h-0.5 w-0 bg-primary-foreground transition-all duration-300 group-hover:w-full"
						></span>
					</a>
				</li>
			{/each}
			<li in:fly={{ y: -20, duration: 400, delay: 400 }}>
				<a
					href="#contact"
					class="rounded-full bg-card px-6 py-2.5 text-sm font-medium text-foreground shadow-soft transition-all duration-300 hover:scale-105 hover:shadow-medium"
				>
					Rezerwacja
				</a>
			</li>
		</ul>

		<button
			onclick={() => (isMobileMenuOpen = !isMobileMenuOpen)}
			class="relative z-10 cursor-pointer p-2 text-primary-foreground md:hidden"
			aria-label="Toggle menu"
		>
			{#if isMobileMenuOpen}
				<X size={24} />
			{:else}
				<Menu size={24} />
			{/if}
		</button>
	</div>

	{#if isMobileMenuOpen}
		<div transition:slide={{ duration: 300 }} class="bg-primary/98 backdrop-blur-lg md:hidden">
			<ul class="container mx-auto flex flex-col gap-4 px-6 py-6">
				{#each navLinks as link (link.href)}
					<li>
						<a
							href={link.href}
							onclick={() => (isMobileMenuOpen = false)}
							class="block py-3 font-body text-lg font-medium text-primary-foreground/90 transition-colors hover:text-primary-foreground"
						>
							{link.label}
						</a>
					</li>
				{/each}
				<li class="pt-4">
					<a
						href="#contact"
						onclick={() => (isMobileMenuOpen = false)}
						class="block w-full rounded-full bg-card px-6 py-3 text-center font-medium text-foreground"
					>
						Rezerwacja
					</a>
				</li>
			</ul>
		</div>
	{/if}
</nav>
