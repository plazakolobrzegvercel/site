<script lang="ts">
	import './layout.css';
	import CookieConsent from '$lib/components/CookieConsent.svelte';

	let { children } = $props();
</script>

{@render children()}
<CookieConsent />
