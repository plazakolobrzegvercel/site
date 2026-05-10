<script>
	export let src = '';
	export let alt = '';
	export let className = '';
	export let width;
	export let height;
	export let loading = 'lazy';
	// simple placeholder + blur-up approach
	let loaded = false;
</script>

<div class={className} style="position:relative;overflow:hidden">
	<img
		{src}
		{alt}
		{loading}
		{width}
		{height}
		class:opacity-0={!loaded}
		on:load={() => (loaded = true)}
		style="width:100%;height:100%;object-fit:cover;transition:opacity 300ms;"
	/>
	{#if !loaded}
		<div
			style="position:absolute;inset:0;background:linear-gradient(90deg,rgba(0,0,0,0.02),rgba(0,0,0,0.04));filter:blur(6px);"
		></div>
	{/if}
</div>
