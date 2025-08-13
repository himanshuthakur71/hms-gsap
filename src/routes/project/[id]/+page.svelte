<script lang="ts">
	import { page } from '$app/state';
	import { projects } from '$lib/jsons/projects.json';
	import { error } from '@sveltejs/kit';
	import gsap from 'gsap';
	import { onMount } from 'svelte';

	let project = projects.find((p: any) => p.id == page.params.id);

	$effect(() => {
		if (!project?.id) {
			throw error(404, 'not found');
		}
	});

	onMount(() => {
		// gsap.to('.projectImage', {
		// 	position: 'fixed',
		// 	width: '100vw',
		// 	height: '100vh',
		// 	inset: '0'
		// });

		// gsap.to('.projectImage', {
        //     delay: 5,
		// 	position: 'static',
        //     duration: 1,
        //     ease: 'power1'
		// });
	});
</script>

<section class="w-full pt-[calc(38.4px+72px)]">
	<div class="px-4">
		<div class="flex w-full items-start justify-between">
			<div>
				<a
					href="/project"
					class="flex size-[48px] items-center justify-center rounded-full bg-white"
				>
					X
				</a>
			</div>

			<div class="">
				<div>
					<p>client</p>
					<p>xxClient Namexx</p>
				</div>
			</div>
		</div>

		<div>
			<h1>xxProjectNamexx</h1>
		</div>
	</div>

	<div class="w-full">
		<figure
			class=" projectImage flex h-screen w-screen items-center justify-center"
			data-flip-id="cover-{project?.id}" data-project-id="123"
		>
			<img src={project?.projectImage} alt="peoject_img" class="h-full w-full" />
		</figure>
	</div>
</section>
