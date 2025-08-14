<script lang="ts">
	import { page } from '$app/state';
	import { projects } from '$lib/jsons/projects.json';
	import { error } from '@sveltejs/kit';
	import gsap from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { onMount } from 'svelte';

	gsap.registerPlugin(ScrollTrigger);

	let project = projects.find((p: any) => p.id == page.params.id);

	$effect(() => {
		if (!project?.id) {
			throw error(404, 'not found');
		}
	});

	onMount(() => {
		// Initial meta info animation
		gsap.from(".metaInfo", {
			y: 40,
			opacity: 0,
			duration: 1,
			stagger: 0.15,
			ease: "power3.out"
		});

		// Title reveal animation
		gsap.from(".projectTitle span", {
			xPercent: -100,
			duration: 1.2,
			delay: 0.2,
			ease: "power4.out"
		});

		// Image entrance animation
		// gsap.from(".projectImage img", {
		// 	scale: 1.15,
		// 	opacity: 0,
		// 	filter: "blur(10px)",
		// 	duration: 1.4,
		// 	delay: 0.4,
		// 	ease: "power2.out"
		// });

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
		<div class="w-full items-start grid grid-cols-[500px_1fr]">
			<div>
				<a href="/project"
					class="flex size-[48px] items-center justify-center rounded-full bg-white">
					X
				</a>
			</div>

			<div class="flex">
				<div class="w-full shrink-0 max-w-[290px] metaInfo">
					<p class="mb-[20px] text-[20px] text-dark-40"><span>Client</span></p>
					<p class="mb-[20px] text-[20px] overflow-hidden"><span>xxClient Namexx</span></p>
				</div>

				<div class="w-full shrink-0 max-w-[290px] metaInfo">
					<p class="mb-[20px] text-[20px] text-dark-40"><span>Services</span></p>
					<p class="mb-[20px] text-[20px] overflow-hidden"><span>Lorem, ipsum.</span></p>
				</div>

				<div class="w-full shrink-0 max-w-[290px] metaInfo">
					<p class="mb-[20px] text-[20px] text-dark-40"><span>Date</span></p>
					<p class="mb-[20px] text-[20px] overflow-hidden"><span>Month YYYY</span></p>
				</div>
			</div>
		</div>

		<div class="pl-[500px] mt-[200px] relative mb-[40px]">
			<h1 class="text-[96px] overflow-hidden projectTitle">
				<span>{project?.title}</span>
			</h1>
		</div>
	</div>

	<div class="w-full">
		<figure class="projectImage flex h-screen w-screen items-center justify-center"
			data-flip-id="cover-{project?.id}" data-project-id="123">
			<img src={project?.projectImage} alt="project_img" class="h-full w-full object-cover" />
		</figure>
	</div>

	<div class="px-4 mt-[140px]">
		<p class="text-[20px] text-brand-ac-2">Project Overview</p>
		<p class="text-[64px]"><span>{project?.description}</span></p>
	</div>
</section>
