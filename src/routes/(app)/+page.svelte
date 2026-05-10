<script>
	import Hero from '$lib/ui/Hero.svelte';
	import Rooms from '$lib/ui/Rooms.svelte';
	import Contact from '$lib/ui/Contact.svelte';
	import About from '$lib/ui/About.svelte';
	import Atmosphere from '$lib/ui/Atmosphere.svelte';
</script>

<svelte:head>
	<title>Plaża Blisko - Komfortowe pokoje gościnne w Kołobrzegu</title>
</svelte:head>

<main class="min-h-screen">
	<Hero />
	<Rooms />
	<About />
	<Atmosphere />
	<Contact />
</main>
