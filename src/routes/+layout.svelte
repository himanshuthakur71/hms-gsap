<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import Header from '$lib/components/Header.svelte';
	import { onMount } from 'svelte';
	import SignatureLoader from '$lib/components/SignatureLoader.svelte';

	let { children } = $props();

	let visible = $state(true);

	onMount(() => {
		visible = true;

		setTimeout(() => {
			visible = false;
		}, 3000);
	});
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
