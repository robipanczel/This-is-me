<script lang="ts">
	import '../app.css';
	import Header from '$lib/header/header.svelte';
	import Footer from '$lib/footer/footer.svelte';
	import { fade } from 'svelte/transition';

	let screenWidth: number;
	let userMenuToggle = false;

	function toggleMenu() {
		userMenuToggle = !userMenuToggle;
	}

	$: isMobileView = screenWidth < 768 ? userMenuToggle : true;
</script>

<div class="flex flex-col min-h-screen bg-gray-500" bind:clientWidth={screenWidth}>
	<div class="flex flex-row">
		{#if isMobileView}
			<div
				transition:fade
				class="{isMobileView
					? 'top-0'
					: '-top-60'} md:relative absolute md:w-64 w-screen md:h-auto h-24 bg-blue-700"
			>
				<Header cssClass="" />
			</div>
		{/if}

		<main class="flex-1 md:w-40 bg-green-700">
			<slot />
		</main>
	</div>

	<Footer cssClass="h-24 bg-red-700" />

	<button class="absolute md:hidden block bottom-10 right-10" on:click|self={toggleMenu}>
		X
	</button>
</div>
