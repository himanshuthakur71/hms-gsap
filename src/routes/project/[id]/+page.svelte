<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { goto } from '$app/navigation';
	import { page } from '$app/state';

	let projectId: any;
	let project;
	let heroImageEl: HTMLDivElement;

	// Example demo projects
	const projects = [
		{
			id: 1,
			title: 'Project One',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=1'
		},
		{
			id: 2,
			title: 'Project Two',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=2'
		},
		{
			id: 3,
			title: 'Project Three',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=3'
		},
		{
			id: 4,
			title: 'Project Four',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=4'
		},
		{
			id: 5,
			title: 'Project Five',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=5'
		},
		{
			id: 6,
			title: 'Project Six',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=6'
		},
		{
			id: 7,
			title: 'Project Seven',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=7'
		},
		{
			id: 8,
			title: 'Project Eight',
			description:
				'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.',
			projectImage: 'https://picsum.photos/600/400?random=8'
		}
	];

		projectId = page.params.id;
		project = projects.find((p) => p.id === Number(projectId));


	onMount(() => {
		// Retrieve transition data from localStorage
		const fromRect = JSON.parse(localStorage.getItem('transitionFrom') || 'null');
		const imgUrl = localStorage.getItem('transitionImage');

		if (fromRect && imgUrl && heroImageEl) {
			// Start image in card's position/size
			gsap.set(heroImageEl, {
				position: 'absolute',
				top: fromRect.top,
				left: fromRect.left,
				width: fromRect.width,
				height: fromRect.height,
				objectFit: 'cover',
				zIndex: 999
			});

			// Animate to fullscreen hero position
			gsap.to(heroImageEl, {
				top: 0,
				left: 0,
				width: window.innerWidth,
				height: 400,
				duration: 0.8,
				ease: 'power3.inOut',
				onComplete: () => {
					gsap.set(heroImageEl, { clearProps: 'all' }); // reset inline styles
				}
			});
		}
	});
</script>

{#if project}
	<div class="relative">
		<!-- Large hero image -->
		<div
			bind:this={heroImageEl}
			class="h-[400px] bg-cover bg-center"
			style={`background-image: url('${project.projectImage}')`}
		></div>

		<!-- Content -->
		<div class="p-6 max-w-4xl mx-auto">
			<h1 class="text-4xl font-bold">{project.title}</h1>
			<p class="mt-2 text-gray-600">{project.description}</p>

			<button
				class="mt-6 px-4 py-2 bg-gray-900 text-white rounded-lg"
				on:click={() => goto('/')}
			>
				Back
			</button>
		</div>
	</div>
{:else}
	<p class="p-6 text-center">Project not found.</p>
{/if}
