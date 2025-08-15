<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { fade } from 'svelte/transition';
	// import { gsap } from 'gsap';
	// import { ScrollTrigger } from 'gsap/ScrollTrigger';

	// gsap.registerPlugin(ScrollTrigger);

	let container: HTMLDivElement;
	let activeProject: (typeof projects)[0] | null = $state(null);

	// Refs for animation
	let projectNameEl: HTMLDivElement | null = $state(null);
	let projectImgEl: HTMLImageElement | null = $state(null);
	let projectNoLeft: any = $state(null);
	let projectNoRight: any = $state(null);

	const projects = [
		{
			id: 1,
			name: 'Shriresume',
			backgroundImage:
				'https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaD_OXLh8WN-LVkLX_Brownvase_1.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90',
			projectImage: 'download.png',
			link: 'https://shriresume.com/'
		},
		{
			id: 2,
			name: 'Shrivivah',
			backgroundImage:
				'https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaC9e-ydWJ-7kSdTn_pool_image-9.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90',
			projectImage: 'shrivivah_bg.png',
			link: 'https://srivivah.com/'
		},
		{
			id: 3,
			name: 'MCIL Society One',
			backgroundImage:
				'https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaC9OFSdWJ-7kSdJK_sc-image-9.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90',
			projectImage: 'mcilsocietyone.png',
			link: 'https://mcilsocietyone.com/'
		}
	];

	let sections: HTMLElement[] = [];

	let sectionObserver :any;

	let containerObserver:any;

	function observeSections() {
		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					const target: any = entry.target as HTMLElement;

					// If the section is NOT intersecting and is the active one → hide
					if (target.dataset.project === activeProject && !entry.isIntersecting) {
						activeProject = null;
					}

					// If any *other* section is at least 20% visible → hide
					if (
						entry.isIntersecting &&
						entry.intersectionRatio >= 0.2 &&
						target.dataset.project !== activeProject
					) {
						activeProject = null;
					}
				});
			},
			{ threshold: [0.05, 0.2, 0.5, 1] } // multiple thresholds for flexibility
		);

		sections.forEach((section) => observer.observe(section));
	}

	let gsap: any, ScrollTrigger: any;

	onMount(async () => {
		const gsapModule = await import('gsap');
		const scrollTriggerModule = await import('gsap/ScrollTrigger');

		gsap = gsapModule.default;
		ScrollTrigger = scrollTriggerModule.default;

		gsap.registerPlugin(ScrollTrigger);

		sectionObserver = new IntersectionObserver(
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

		containerObserver = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (!entry.isIntersecting) {
						activeProject = null; // Hide overlay when container is out of view
					}
				});
			},
			{ threshold: 0.2 }
		);

		document.querySelectorAll('.project-section').forEach((section) => {
			sectionObserver.observe(section);
		});

		if (container) containerObserver.observe(container);

		
	});

	onDestroy(() => {
			document.querySelectorAll('.project-section').forEach((section) => {
				sectionObserver.unobserve(section);
			});
			if (container) containerObserver.unobserve(container);
		});

	// 🔹 Equivalent to afterUpdate in runes mode
	$effect(() => {
		if (activeProject && projectNameEl && projectImgEl) {
			// Animate project name
			gsap.fromTo(
				projectNameEl,
				{ opacity: 0, x: -50 },
				{ opacity: 1, x: 0, duration: 0.6, ease: 'power2.out' }
			);

			// Animate project image
			gsap.fromTo(
				projectImgEl,
				{ opacity: 0, scale: 0.1, rotate: -5 },
				{ opacity: 1, scale: 1, rotate: 0, duration: 3, ease: 'elastic.out(1, 0.6)' }
			);

			// Animate project No
			gsap.fromTo(
				projectNoLeft,
				{ opacity: 0, x: -100 },
				{ opacity: 1, x: 0, duration: 0.6, ease: 'power2.out' }
			);

			gsap.fromTo(
				projectNoRight,
				{ opacity: 0, x: 100 },
				{ opacity: 1, x: 0, duration: 0.6, ease: 'power2.out' }
			);
		}
	});

	const handleMouse = (e: any) => {
		gsap.to('#cursor', {
			x: e.x,
			y: e.y,
			duration: 0.4
		});
	};
</script>

<div
	role="presentation"
	bind:this={container}
	class="group relative min-h-screen w-full"
	id="projects"
	onmousemove={handleMouse}
>
	<!-- Parallax Sections -->
	<div class="w-full">
		{#each projects as project}
			<div
				class="project-section relative flex h-screen w-full items-center justify-center overflow-hidden"
				data-id={project.id}
			>
				<div
					class="absolute inset-0 bg-cover bg-fixed bg-center"
					style={`background-image: url(${project.backgroundImage});`}
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
			<div bind:this={projectNameEl} class=" absolute pl-[34%]  top-[23%] text-center lg:top-[unset] lg:pl-0 lg:left-4 text-lg lg:text-3xl font-semibold text-white">
				{activeProject.name}
			</div>

			<!-- Project image circle -->
			<div
				transition:fade
				class="relative mx-auto flex  size-[280px] md:size-[350px] items-center justify-center overflow-hidden rounded-full border-[2px] border-white p-12 transition-opacity duration-300"
			>
				<span class=" absolute top-[20px] z-10 text-[16px] font-semibold text-white"
					>Fetured Work</span
				>

				<span
					bind:this={projectNoLeft}
					class=" absolute top-[50%] left-[20px] z-10 inline-block overflow-hidden text-[16px] font-semibold text-white"
				>
					<i>0{activeProject?.id}</i>
				</span>
				<span
					bind:this={projectNoRight}
					class=" absolute top-[50%] right-[20px] z-10 text-[16px] font-semibold text-white"
					>0{activeProject?.id}</span
				>
				<span class=" absolute bottom-[20px] z-10 text-[16px] font-semibold text-white">Scroll</span
				>
				<div class="flex h-full w-full items-center justify-center rounded-full bg-transparent p-2">
					<figure
						class="flex h-full w-full items-center justify-center overflow-hidden rounded-full bg-amber-200 p-2"
					>
						<img
							bind:this={projectImgEl}
							src={`/images/${activeProject.projectImage}`}
							alt={activeProject.name}
							class=" flex h-full w-full rounded-full bg-white"
						/>
					</figure>
				</div>
			</div>

			<div></div>
		</div>
	{/if}

	<div
		id="cursor"
		class=" fixed top-0 z-[999] hidden flex-col items-center justify-center gap-1 group-hover:flex"
	>
		<figure class=" flex size-[45px] items-center justify-center rounded-full bg-white">
			<svg
				class="shrink-0"
				id="f2"
				xmlns="http://www.w3.org/2000/svg"
				width="13"
				height="13"
				fill="none"
				viewBox="0 0 13 13"
			>
				<path
					stroke="currentColor"
					stroke-width="1.5"
					d="m5.677 1 5.657 5.657m0 0-5.657 5.657m5.657-5.657H.02"
				></path>
			</svg>
		</figure>
		<span class=" text-[14px] font-thin text-white">View Project</span>
	</div>
</div>
