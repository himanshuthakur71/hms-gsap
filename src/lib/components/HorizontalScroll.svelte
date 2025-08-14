<script lang="ts">
	import { onMount } from 'svelte';
	// import { gsap } from 'gsap';
	// import { ScrollTrigger } from 'gsap/ScrollTrigger';

	let { children } = $props();

	// gsap.registerPlugin(ScrollTrigger);

	let horizontalSection: any = $state(null);

	let gsap, ScrollTrigger;

	onMount(async () => {
		const gsapModule = await import('gsap');
		const scrollTriggerModule = await import('gsap/ScrollTrigger');

		gsap = gsapModule.default;
		ScrollTrigger = scrollTriggerModule.default;

		gsap.registerPlugin(ScrollTrigger);

		const container: any = horizontalSection;
		const panels: any = gsap.utils.toArray('.pannel-hozi');

		// Horizontal scroll effect
		gsap.to(panels, {
			xPercent: -100 * (panels.length - 1),
			ease: 'none',
			scrollTrigger: {
				trigger: container,
				pin: true,
				scrub: 1,
				snap: 1 / (panels.length - 1),
				end: () => '+=' + container.offsetWidth
			}
		});
	});
</script>

<section bind:this={horizontalSection} class="horizontal-section flex w-full">
	{@render children()}
</section>
