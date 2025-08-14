<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	// import gsap from 'gsap';
	// import ScrollTrigger from 'gsap/ScrollTrigger';

	// gsap.registerPlugin(ScrollTrigger);

	let sectionEl45: HTMLElement;
	let imgWrap: HTMLElement;

	let gsap:any, ScrollTrigger:any;

	onMount( async () => {

		const gsapModule = await import('gsap');
		const scrollTriggerModule = await import('gsap/ScrollTrigger');

		gsap = gsapModule.default;
		ScrollTrigger = scrollTriggerModule.default;

		gsap.registerPlugin(ScrollTrigger);

		if (!sectionEl45) return;

		// Initial stagger animations for text + lists
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: sectionEl45,
				start: 'top 60%',
				toggleActions: 'restart none restart none'
				// markers: true
			}
		});

		tl.from('#listElc li', {
			x: -50,
			opacity: 0,
			duration: 0.5,
			stagger: 0.15,
			ease: 'power2.out'
		})
			.from('#containerEl .lineChild > div', {
				yPercent: 100,
				opacity: 0,
				duration: 0.6,
				stagger: 0.05,
				ease: 'power3.out'
			}, "-=0.3");

		// Image reveal animation before parallax starts
		const figures = imgWrap.querySelectorAll('figure img');

		gsap.from(figures, {
			scale: 1.05,
			opacity: 0,
			duration: 1,
			ease: 'power2.out',
			stagger: 0.2,
			scrollTrigger: {
				trigger: imgWrap,
				start: 'top 80%',
				toggleActions: 'play none none reverse'
			}
		});

		// Parallax effect with smooth scrub
		gsap.to(figures[0], {
			yPercent: -15,
			ease: 'none',
			scrollTrigger: {
				trigger: sectionEl45,
				start: 'top bottom',
				end: 'bottom top',
				scrub: 1.2
			}
		});

		gsap.to(figures[1], {
			yPercent: 15,
			ease: 'none',
			scrollTrigger: {
				trigger: sectionEl45,
				start: 'top bottom',
				end: 'bottom top',
				scrub: 1.2
			}
		});
	});
</script>


<section bind:this={sectionEl45} class="w-full py-32">
	<div class="grid w-full grid-cols-1 px-4 lg:grid-cols-2">
		<div class="w-full">
			<ul class="w-full max-w-[356px] border-t-[1px] border-dark-10" id="listElc">
				{#each Array(4) as _, i}
					<li class="flex items-center gap-[25px] border-b-[1px] border-dark-10 py-[19px]">
						<span
							class=" flex size-[25px] items-center justify-center rounded-full bg-brand-ac-3 text-[11.2px]"
							>{i + 1}</span
						>
						<span>Lorem ipsum dolor sit.</span>
					</li>
				{/each}
			</ul>
		</div>
		<div class="w-full" id="containerEl">
			<p class="flex items-center gap-[15px]">
				<span class="flex size-[5px] items-center justify-center rounded-full bg-brand-ac-2"></span>
				<span class="inline-block overflow-hidden text-[14.4px] text-brand-ac-2">
					<span id="ani1">From idea to impact</span>
				</span>
			</p>

			<h4 class=" mt-[20px] mb-[25px] text-[51.2px] leading-[64px] text-brand-dark" style="">
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">Designing</div>
						<div style="position:relative;display:inline-block;">Experiences</div>
						<div style="position:relative;display:inline-block;">That</div>
					</div>
				</div>
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">Resonate</div>
						<div style="position:relative;display:inline-block;">and</div>
						<div style="position:relative;display:inline-block;">Scale</div>
					</div>
				</div>
			</h4>

			<div class=" mb-[96px] w-full max-w-[356px] text-[16px] text-dark-50" style="">
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">Every</div>
						<div style="position:relative;display:inline-block;">detail</div>
						<div style="position:relative;display:inline-block;">we</div>
						<div style="position:relative;display:inline-block;">design,</div>
						<div style="position:relative;display:inline-block;">from</div>
						<div style="position:relative;display:inline-block;">a</div>
						<div style="position:relative;display:inline-block;">color</div>
						<div style="position:relative;display:inline-block;">system</div>
						<div style="position:relative;display:inline-block;">to</div>
						<div style="position:relative;display:inline-block;">a</div>
					</div>
				</div>
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">dashboard</div>
						<div style="position:relative;display:inline-block;">layout,</div>
						<div style="position:relative;display:inline-block;">is</div>
						<div style="position:relative;display:inline-block;">rooted</div>
						<div style="position:relative;display:inline-block;">in</div>
						<div style="position:relative;display:inline-block;">user</div>
						<div style="position:relative;display:inline-block;">behavior,</div>
					</div>
				</div>
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">business</div>
						<div style="position:relative;display:inline-block;">goals,</div>
						<div style="position:relative;display:inline-block;">and</div>
						<div style="position:relative;display:inline-block;">the</div>
						<div style="position:relative;display:inline-block;">belief</div>
						<div style="position:relative;display:inline-block;">that</div>
						<div style="position:relative;display:inline-block;">good</div>
						<div style="position:relative;display:inline-block;">design</div>
					</div>
				</div>
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">should</div>
						<div style="position:relative;display:inline-block;">feel</div>
						<div style="position:relative;display:inline-block;">effortless.</div>
						<div style="position:relative;display:inline-block;">We</div>
						<div style="position:relative;display:inline-block;">blend</div>
						<div style="position:relative;display:inline-block;">strategy</div>
						<div style="position:relative;display:inline-block;">and</div>
						<div style="position:relative;display:inline-block;">craft</div>
					</div>
				</div>
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">to</div>
						<div style="position:relative;display:inline-block;">deliver</div>
						<div style="position:relative;display:inline-block;">experiences</div>
						<div style="position:relative;display:inline-block;">that</div>
						<div style="position:relative;display:inline-block;">scale</div>
						<div style="position:relative;display:inline-block;">beautifully</div>
						<div style="position:relative;display:inline-block;">and</div>
					</div>
				</div>
				<div class="lineParent" style="display: block; text-align: start; position: relative;">
					<div
						class="lineChild"
						style="display: block; text-align: start; position: relative; translate: none; rotate: none; scale: none; transform: translate(0px, 0%); will-change: auto;"
					>
						<div style="position:relative;display:inline-block;">work</div>
						<div style="position:relative;display:inline-block;">seamlessly</div>
						<div style="position:relative;display:inline-block;">across</div>
						<div style="position:relative;display:inline-block;">platforms.</div>
					</div>
				</div>
			</div>
		</div>
	</div>
	<div class="grid w-full grid-cols-1 px-4 lg:grid-cols-2" bind:this={imgWrap}>
		<div class="w-full">
			<figure
				class="flex h-[416px] w-[356px] items-center justify-center overflow-hidden rounded-lg"
			>
				<img
					src="https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaEABd7h8WN-LVklA_Home3.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90"
					alt="img"
					class="h-full w-full object-cover"
				/>
			</figure>
		</div>

		<div class="w-full">
			<figure
				class="flex h-[864px] w-[728px] items-center justify-center overflow-hidden rounded-lg"
			>
				<img
					src="https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaEABMLh8WN-LVkk8_Home-4.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90"
					alt="img"
					class="h-full w-full object-cover"
				/>
			</figure>
		</div>
	</div>
</section>

<style>
	figure img {
		will-change: transform;
	}
</style>
