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

<div class="flex flex-col min-h-screen bg-black" bind:clientWidth={screenWidth}>
	<div class="flex flex-row flex-1">
		{#if isMobileView}
			<div
				transition:fade
				class="{isMobileView
					? 'top-0'
					: '-top-60'} md:relative absolute md:w-64 w-screen md:h-auto h-24 menu-bg"
			>
				<Header cssClass="" />
			</div>
		{/if}

		<main class="flex-1 md:w-40 body-bg">
			<slot />
		</main>
	</div>

	<div class="h-24 footer-bg">
		<Footer cssClass="" />
	</div>

	<button class="absolute md:hidden block bottom-10 right-10" on:click|self={toggleMenu}>
		X
	</button>
</div>

<style>
	.body-bg {
		background-color: #e6e6e9;
	}

	.menu-bg {
		background-color: #9999a1;
	}

	.footer-bg {
		background-color: #66666e;
	}
</style>
