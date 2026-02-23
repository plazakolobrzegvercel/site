<script lang="ts">
	import { fly } from 'svelte/transition';
	import { Waves, Heart } from '@lucide/svelte';
	import logo from '$lib/assets/logo.avif';

	const currentYear = new Date().getFullYear();

	const navLinks = [
		{ href: '#home', label: 'Start' },
		{ href: '#about', label: 'O nas' },
		{ href: '#rooms', label: 'Pokoje' },
		{ href: '#contact', label: 'Kontakt' }
	];

	let visible = $state(false);

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

<footer class="relative overflow-hidden bg-primary py-12 text-primary-foreground">
	<div
		class="bg-gradient-sand absolute top-0 right-0 left-0 h-16"
		style="clip-path: ellipse(60% 100% at 50% 0%)"
	></div>

	<div
		use:inview={() => (visible = true)}
		class="relative z-10 container mx-auto max-w-350 px-6 pt-8"
	>
		{#if visible}
			<div class="flex flex-col items-center justify-between gap-8 md:flex-row">
				<div transition:fly={{ y: 20, duration: 500 }} class="text-center md:text-left">
					<img
						src={logo}
						alt="Plaza Blisko"
						class="mx-auto mb-4 h-16 w-auto opacity-90 brightness-0 invert md:mx-0"
					/>
					<p class="max-w-xs font-body text-sm text-primary-foreground/70">
						Pokoje gościnne w Kołobrzegu, zaledwie 150m od plaży. Idealne miejsce na Twój wakacyjny
						wypoczynek.
					</p>
				</div>

				<nav transition:fly={{ y: 20, duration: 500, delay: 100 }} class="flex gap-8">
					{#each navLinks as link, i (i)}
						<a
							href={link.href}
							class="font-body text-sm text-primary-foreground/70 transition-colors hover:text-primary-foreground"
						>
							{link.label}
						</a>
					{/each}
				</nav>

				<div
					transition:fly={{ y: 20, duration: 500, delay: 200 }}
					class="text-center md:text-right"
				>
					<a
						href="tel:+48502258401"
						class="font-display text-xl text-primary-foreground transition-colors hover:text-cream"
					>
						502 258 401
					</a>
					<p class="mt-1 font-body text-sm text-primary-foreground/70">rezerwacje@plazablisko.pl</p>
				</div>
			</div>

			<div class="my-8 h-px bg-primary-foreground/20"></div>

			<div class="flex flex-col items-center justify-between gap-4 md:flex-row">
				<p class="flex items-center gap-2 font-body text-xs text-primary-foreground/60">
					<Waves class="h-4 w-4" />
					© {currentYear} Plaza Blisko. Wszelkie prawa zastrzeżone.
				</p>
				<p class="flex items-center gap-1 font-body text-xs text-primary-foreground/60">
					Stworzone z <Heart class="h-3 w-3 text-sunset" /> w Kołobrzegu
				</p>
			</div>
		{/if}
	</div>
</footer>
