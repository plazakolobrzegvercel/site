<script lang="ts">
	import { X } from '@lucide/svelte';

	let accepted = false;
	let visible = true;

	function acceptCookies() {
		accepted = true;
		visible = false;
		localStorage.setItem('cookieConsent', 'accepted');
	}

	function closeBanner() {
		visible = false;
		localStorage.setItem('cookieConsent', 'dismissed');
	}

	function checkConsent() {
		const consent = localStorage.getItem('cookieConsent');
		if (consent) {
			visible = false;
		}
	}

	if (typeof window !== 'undefined') {
		checkConsent();
	}
</script>

{#if visible}
	<div class="fixed right-0 bottom-0 left-0 z-40 bg-primary/95 px-4 py-4 backdrop-blur-sm">
		<div class="container mx-auto max-w-screen-xl">
			<div class="flex flex-col items-center justify-between gap-4 md:flex-row">
				<div class="flex-1">
					<p class="text-sm text-primary-foreground/90">
						Używamy plików cookies i RODO, aby zapewnić Ci najlepsze doświadczenie na naszej
						stronie. Kontynuując przeglądanie, wyrażasz zgodę na naszą
						<a href="/informacje#regulamin" class="underline hover:text-primary-foreground">
							politykę prywatności
						</a>
						.
					</p>
				</div>
				<div class="flex gap-3">
					<button
						type="button"
						onclick={closeBanner}
						class="rounded-full bg-card/50 px-5 py-2 text-sm font-medium text-foreground transition-all hover:bg-card"
					>
						Nie akceptuję
					</button>
					<button
						type="button"
						onclick={acceptCookies}
						class="bg-gradient-sea rounded-full px-5 py-2 text-sm font-medium text-primary-foreground transition-all hover:shadow-glow"
					>
						Akceptuję
					</button>
				</div>
				<button
					type="button"
					onclick={closeBanner}
					class="absolute top-3 right-3 p-1 text-primary-foreground/70 hover:text-primary-foreground md:hidden"
				>
					<X size={20} />
				</button>
			</div>
		</div>
	</div>
{/if}
