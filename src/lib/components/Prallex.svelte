<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { fade } from 'svelte/transition';

	let container: HTMLDivElement;
	let activeProject: (typeof projects)[0] | null = null;

	const projects = [
		{
			id: 1,
			name: 'Shriresume',
			backgroundImage: 'download.png',
			projectImage: 'logo-shriresume.webp',
			link: 'https://shriresume.com/'
		},
		{
			id: 2,
			name: 'Shrivivah',
			backgroundImage: 'shrivivah_bg.png',
			projectImage: 'shrivivah_logo.png',
			link: 'https://srivivah.com/'
		},
		{
			id: 3,
			name: 'MCIL Society One',
			backgroundImage: 'mcilsocietyone.png',
			projectImage: 'mcilsocietyoneLogo.svg',
			link: 'https://mcilsocietyone.com/'
		}
	];

	onMount(() => {
		const sectionObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						const id = Number(entry.target.getAttribute('data-id'));
						activeProject = projects.find((p) => p.id === id) || null;
					}
				});
			},
			{ threshold: 0.5 }
		);

		const containerObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (!entry.isIntersecting) {
						activeProject = null; // Hide overlay when container is out of view
					}
				});
			},
			{ threshold: 0.05 }
		);

		document.querySelectorAll('.project-section').forEach((section) => {
			sectionObserver.observe(section);
		});

		if (container) containerObserver.observe(container);

		onDestroy(() => {
			document.querySelectorAll('.project-section').forEach((section) => {
				sectionObserver.unobserve(section);
			});
			if (container) containerObserver.unobserve(container);
		});
	});
</script>

<div bind:this={container} class="relative min-h-screen w-full">
	<!-- Parallax Sections -->
	<div class="w-full">
		{#each projects as project}
			<div
				class="project-section relative flex h-screen w-full items-center justify-center overflow-hidden"
				data-id={project.id}
			>
				<div
					class="absolute inset-0 bg-cover bg-fixed bg-center"
					style={`background-image: url(/images/${project.backgroundImage});`}
				></div>
			</div>
		{/each}
	</div>

	<!-- Dark overlay -->
	<div class="absolute inset-0 h-full w-full bg-black/70"></div>

	<!-- Fixed Overlay -->
	{#if activeProject}
		<div
			class="fixed inset-0 z-50 flex h-full min-h-screen w-full items-center justify-between px-4 transition-opacity duration-300"
		>
			<!-- Project name -->
			<div class="absolute text-3xl font-semibold text-white">{activeProject.name}</div>

			<!-- Project image circle -->
			<div
				transition:fade
				class="mx-auto flex size-[350px] items-center justify-center overflow-hidden rounded-full border-[2px] border-white p-2 transition-opacity duration-300"
			>
				<div class="flex h-full w-full items-center justify-center rounded-full bg-transparent p-2">
					<figure
						class="flex h-full w-full items-center justify-center overflow-hidden rounded-full bg-amber-200 p-4"
					>
						<img
							src={`/images/${activeProject.backgroundImage}`}
							alt={activeProject.name}
							class=" flex h-full w-full rounded-full bg-white"
						/>
					</figure>
				</div>
			</div>

			<div></div>
		</div>
	{/if}
</div>
