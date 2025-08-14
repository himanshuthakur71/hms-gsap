<script lang="ts">
	import { page } from '$app/state';
	import { projects } from '$lib/jsons/projects.json';
	import { error } from '@sveltejs/kit';
	// import gsap from 'gsap';
	// import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { onMount } from 'svelte';

	// gsap.registerPlugin(ScrollTrigger);

	let project = projects.find((p: any) => p.id == page.params.id);

	let gsap: any, ScrollTrigger: any;

	$effect(() => {
		if (!project?.id) {
			throw error(404, 'not found');
		}
	});

	onMount(async () => {
		const gsapModule = await import('gsap');
		const scrollTriggerModule = await import('gsap/ScrollTrigger');

		gsap = gsapModule.default;
		ScrollTrigger = scrollTriggerModule.default;

		gsap.registerPlugin(ScrollTrigger);

		
		let tl2Y6 = gsap.timeline()


		// Image entrance animation
		tl2Y6.from('.projectImage', {
			yPercent: -100,
			zIndex: '999',
			duration: 2,
			// delay: 0.4,
			ease: 'power2.out'
		});

		// Initial meta info animation
		tl2Y6.from('.metaInfo', {
			y: 40,
			opacity: 0,
			duration: 1,
			stagger: 0.15,
			ease: 'power3.out'
		});

		// Title reveal animation
		tl2Y6.from('#projectTitle', {
			y: 100,
			duration: 1.2,
			delay: 0.2,
			ease: 'power4.out'
		});

		

		// Scroll-triggered fade out of image
		// gsap.to(".projectImage", {
		// 	scrollTrigger: {
		// 		trigger: ".projectImage",
		// 		start: "top top",
		// 		end: "bottom top",
		// 		scrub: true
		// 	},
		// 	scale: 0.95,
		// 	opacity: 0.4
		// });
	});
</script>

<section class="w-full pt-[calc(38.4px+72px)]">
	<div class="px-4">
		<div class="grid w-full grid-cols-1 items-start gap-y-6 lg:grid-cols-[500px_1fr]">
			<div>
				<a
					href="/project"
					class="flex size-[48px] items-center justify-center rounded-full bg-white"
				>
					X
				</a>
			</div>

			<div class="flex flex-wrap">
				<div class="metaInfo w-full max-w-[290px] shrink-0">
					<p class="mb-[20px] text-[20px] text-dark-40"><span>Client</span></p>
					<p class="mb-[20px] overflow-hidden text-[20px]"><span>xxClient Namexx</span></p>
				</div>

				<div class="metaInfo w-full max-w-[290px] shrink-0">
					<p class="mb-[20px] text-[20px] text-dark-40"><span>Services</span></p>
					<p class="mb-[20px] overflow-hidden text-[20px]"><span>Lorem, ipsum.</span></p>
				</div>

				<div class="metaInfo w-full max-w-[290px] shrink-0">
					<p class="mb-[20px] text-[20px] text-dark-40"><span>Date</span></p>
					<p class="mb-[20px] overflow-hidden text-[20px]"><span>Month YYYY</span></p>
				</div>
			</div>
		</div>

		<div class="relative mt-[200px] mb-[40px] lg:pl-[500px]">
			<h1 class="projectTitle overflow-hidden text-[96px] inline-block">
				<span id="projectTitle">{project?.title}</span>
			</h1>
		</div>
	</div>

	<div class="w-full">
		<figure
			class="projectImage flex h-screen w-screen items-center justify-center"
			data-flip-id="cover-{project?.id}"
			data-project-id="123"
		>
			<img src={project?.projectImage} alt="project_img" class="h-full w-full object-cover" />
		</figure>
	</div>

	<div class="mt-[140px] px-4">
		<p class="text-[18px] lg:text-[20px] text-brand-ac-2">Project Overview</p>
		<p class="text-[32px] lg:text-[64px]"><span>{project?.description}</span></p>
	</div>
</section>
