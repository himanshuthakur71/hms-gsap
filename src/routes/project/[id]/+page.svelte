<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { page } from '$app/state';


	let imageUrl: string | null = null;
	let fromRect: DOMRect | null = null;
	let imgEl: HTMLImageElement;
	let projectId: string;

	// Get project data (demo)
	const projects = [
		{
			id: 1,
			title: 'Project One',
			description: 'A short description of project one.',
			projectImage: 'https://picsum.photos/1200/800?random=1'
		},
		{
			id: 2,
			title: 'Project Two',
			description: 'Another exciting project.',
			projectImage: 'https://picsum.photos/1200/800?random=2'
		}
	];

	let project: typeof projects[0] | undefined;

	onMount(() => {
		projectId = page.params.id;
		project = projects.find(p => p.id.toString() === projectId);

		imageUrl = localStorage.getItem('transitionImage');
		const rectData = localStorage.getItem('transitionFrom');
		if (rectData) {
			fromRect = JSON.parse(rectData);
		}

		if (imageUrl && fromRect && imgEl) {
			// Start image at previous page position
			gsap.set(imgEl, {
				position: 'absolute',
				top: fromRect.top,
				left: fromRect.left,
				width: fromRect.width,
				height: fromRect.height,
				objectFit: 'cover'
			});

			// Animate into place
			gsap.to(imgEl, {
				top: 0,
				left: 0,
				width: '100%',
				height: '60vh',
				duration: 0.8,
				ease: 'power3.inOut'
			});
		} else {
			// Fallback if no transition data
			if (imgEl) {
				gsap.set(imgEl, {
					width: '100%',
					height: '60vh'
				});
			}
		}
	});
</script>

<div class="relative w-full overflow-hidden">
	{#if imageUrl}
		<img bind:this={imgEl} src={imageUrl} alt="Project_Image" class="rounded-b-xl" />
	{:else if project}
		<img bind:this={imgEl} src={project.projectImage} alt={project.title} class="rounded-b-xl" />
	{/if}

	<!-- Overlay and Title -->
	<div class="absolute bottom-6 left-6 text-white drop-shadow-lg">
		<h1 class="text-4xl font-bold">{project?.title}</h1>
		<p class="mt-2 max-w-lg">{project?.description}</p>
	</div>
</div>

<section class="p-6 max-w-4xl mx-auto">
	<h2 class="text-2xl font-semibold mb-4">Project Details</h2>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
	</p>
</section>
