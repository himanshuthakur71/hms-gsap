<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { fade } from 'svelte/transition';

	let container: HTMLDivElement;
	let showFixed = $state(false);

	const projects = [
		{
			id: 1,
			name: 'Shriresume',
			backgroundImage: '/download.png',
			projectImage: '/logo-shriresume.webp',
			link: 'https://shriresume.com/'
		},
		{
			id: 2,
			name: 'Shrivivah',
			backgroundImage: '/shrivivah_bg.png',
			projectImage: '/shrivivah_logo.png',
			link: 'https://srivivah.com/'
		},
		{
			id: 1,
			name: 'MCIL Society One',
			backgroundImage: '/mcilsocietyone.png',
			projectImage: '/mcilsocietyoneLogo.svg',
			link: 'https://mcilsocietyone.com/'
		}
	];

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					showFixed = entry.isIntersecting;
				});
			},
			{
				threshold: 0.2 // Show when at least 20% of the component is visible
			}
		);

		if (container) observer.observe(container);

		onDestroy(() => {
			if (container) observer.unobserve(container);
		});
	});
</script>

<div bind:this={container} class="relative min-h-screen w-full">
	<div class="w-full">
		{#each projects as project}
			<div class="relative flex h-screen w-full items-center justify-center overflow-hidden">
				<div
					class="absolute inset-0 bg-cover bg-fixed bg-center"
					style={`background-image: url(/images/${project?.backgroundImage});`}
				></div>
			</div>
		{/each}
	</div>

	<div class="absolute inset-0 h-full w-full bg-black/70"></div>

	{#if showFixed}
		<div
			class="fixed inset-0 z-50 flex h-full min-h-screen w-full items-center justify-between px-4 transition-opacity duration-300"
		>
			<div class=" text-3xl font-semibold text-white">Project Name</div>

			<div
				transition:fade
				class="flex size-[350px] items-center justify-center overflow-hidden rounded-full border-[2px] border-white p-2 transition-opacity duration-300"
			>
				<div
					class=" flex h-full w-full items-center justify-center rounded-full bg-transparent p-2"
				>
					<figure
						class=" h-full w-full items-center justify-center overflow-hidden rounded-full bg-red-50"
					>
						<img
							src="https://fastly.picsum.photos/id/1015/1920/1080.jpg?hmac=M12OSFAxxiMvlGq9OtLXHs02DhW37fZ72Ui-DHvRI28"
							alt=""
							class=" h-full w-full"
						/>
					</figure>
				</div>
			</div>

			<div></div>
		</div>
	{/if}
</div>
