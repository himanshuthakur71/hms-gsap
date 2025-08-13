<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import Header from '$lib/components/Header.svelte';
	import { onMount, tick } from 'svelte';
	import SignatureLoader from '$lib/components/SignatureLoader.svelte';
	import { navigating } from '$app/state';

	let { children } = $props();

	let visible = $state(true);

	// Show loader on initial mount
	onMount(() => {
		showLoader();
	});

	// Watch for navigation events
	$effect(() => {
		if (navigating.to) {
			// showLoader();
		}
	});

	async function showLoader() {
		visible = true;
		await tick(); // ensures DOM updates before timeout
		setTimeout(() => {
			visible = false;
		}, 3000); // adjust duration as needed
	}
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{#if visible}
	<SignatureLoader />
{:else}
	<div class="w-full">
		<Header />
		<main>
			{@render children?.()}
		</main>
	</div>
{/if}
