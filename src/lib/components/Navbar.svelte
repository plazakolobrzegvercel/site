<script>
	import { onMount } from 'svelte';
	import { slide, fade } from 'svelte/transition';
	import { Menu, X } from '@lucide/svelte';

	const navLinks = [
		{ href: '#home', label: 'Start' },
		{ href: '#about', label: 'O nas' },
		{ href: '#rooms', label: 'Pokoje' },
		{ href: '#contact', label: 'Kontakt' },
		{ href: '/informacje#regulamin', label: 'Regulamin', isRoute: true }
	];

	let isScrolled = false;
	let isMobileMenuOpen = false;

	onMount(() => {
		const handleScroll = () => {
			isScrolled = window.scrollY > 50;
		};
		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});
</script>

<header
	class={`fixed top-0 right-0 left-0 z-50 transition-all duration-500 ${
		isScrolled
			? 'bg-primary/95 py-4 shadow-medium backdrop-blur-md md:py-3'
			: 'bg-primary/90 py-6 backdrop-blur-sm md:py-6'
	}`}
>
	<nav class="relative container mx-auto flex items-center justify-center px-6">
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
		<div class="bg-primary/98 backdrop-blur-lg md:hidden">
			<ul class="container mx-auto flex flex-col gap-2 px-6 py-6">
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
